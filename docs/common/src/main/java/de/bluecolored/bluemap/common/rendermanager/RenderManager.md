# RenderManager.java

## Přehled

`RenderManager` je centrální orchestrátor renderovacího procesu v BlueMap. Spravuje frontu úloh (`RenderTask`) a sadu
pracovních vláken (`WorkerThread`), která tyto úlohy paralelně vykonávají. Jeho hlavním úkolem je efektivně vytěžovat
CPU při zachování plynulosti a možnosti dynamického přidávání prioritních úloh.

## Umístění

`de.bluecolored.bluemap.common.rendermanager.RenderManager`

## Balíček

`de.bluecolored.bluemap.common.rendermanager`

## Atributy a Stavové Proměnné

### Správa Vláken

- `workerThreads`: Kolekce aktivních `WorkerThread` instancí.
- `busyCount`: `AtomicInteger` počítající vlákna, která právě provádějí metodu `doWork()` na nějaké úloze.
- `running`: `volatile boolean` určující, zda manažer běží.

### Fronta Úloh

- `renderTasks`: `LinkedList<RenderTask>` fungující jako FIFO fronta. První prvek je úloha, na které se právě pracuje.
- `completedTasks`: `LinkedHashMap` uchovávající posledních 10 dokončených úloh pro statistické účely.

### Sledování Postupu

- `progressTracker`: Instance `ProgressTracker` pro odhad rychlosti a zbývajícího času.
- `newTask`: Příznak, že byla vybrána nová úloha z fronty, což vyžaduje reset trackeru.

## Vnitřní třída `WorkerThread`

Dědí od `Thread`. Každé vlákno v nekonečné smyčce volá `RenderManager.this.doWork()`, dokud je manažer v stavu
`running`.

- **Ošetření chyb:** Pokud při práci dojde k výjimce, vlákno chybu zaloguje a na 10 sekund se uspí. To zabraňuje
  cyklickému "pádu na plný plyn", pokud je problém např. v přístupu k souborům.
- **Priority:** Vlákna mají nastavitelnou prioritu (standardně nízkou, aby neovlivňovala chod Minecraft serveru).

## Vnitřní Logika a Metody

### `start(int threadCount, int threadPriority)`

1. Zajistí, že manažer ještě neběží.
2. Inicializuje `ProgressTracker`.
3. Vytvoří a spustí zadaný počet vláken. Nastaví jim jméno `BlueMap-RenderThread-{managerId}-{threadId}`.

### `doWork()` (Privátní, voláno worker thready)

Toto je nejdůležitější metoda pro pochopení paralelismu v BlueMap:

1. **Čekání na práci:** Pokud je fronta prázdná, vlákno se uspí na `renderTasks.wait(10000)`.
2. **Výběr úlohy:** Vezme první úlohu ve frontě (`renderTasks.getFirst()`).
3. **Kontrola dokončení úlohy:** Pokud `!task.hasMoreWork()`:
    - Vlákno musí počkat, až **všechna ostatní vlákna** (`busyCount == 0`) dokončí svou část práce na této úloze.
    - Poté první vlákno, které si toho všimne, úlohu definitivně odstraní z fronty, přesune do `completedTasks` a
      nastaví `newTask = true`.
4. **Vlastní práce:**
    - Inkrementuje `busyCount`.
    - Zavolá `task.doWork()`. **Pozor:** Více vláken volá `doWork()` na téže instanci úlohy (např.
      `WorldRegionRenderTask`). Tato úloha musí být na takové volání navržena (thread-safe).
    - Po návratu z `doWork()` dekrementuje `busyCount` a zavolá `notifyAll()`.

### Správa Fronty (Scheduling)

Manažer implementuje chytrou logiku pro přidávání úloh:

- **`scheduleRenderTask(task)`**: Přidá úlohu na konec.
- **`scheduleRenderTaskNext(task)`**: Přidá úlohu na druhou pozici (hned za aktuálně rozpracovanou).
- **Deduplikace (`containsRenderTask`)**: Před přidáním zkontroluje, zda identická úloha (nebo úloha, která ji obsahuje)
  již ve frontě není.
- **Inkluze (`removeTasksThatAreContainedIn`)**: Pokud přidáváte např. "Update celého světa" a ve frontě jsou "Update
  regionu A" a "Update regionu B", tyto menší úlohy jsou automaticky odstraněny (zrušeny), protože jsou zahrnuty v té
  nové.

### Pomocné Metody

- `awaitIdle()`: Blokuje vlákno, dokud není fronta úloh prázdná.
- `stop()`: Nastaví `running = false` a přeruší všechna pracovní vlákna.
- `estimateCurrentRenderTaskTimeRemaining()`: Vypočítá zbývající čas na základě `ProgressTracker`u a zbývajícího
  postupu (1 - progress).
