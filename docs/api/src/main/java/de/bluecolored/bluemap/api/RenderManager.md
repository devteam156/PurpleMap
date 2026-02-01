# RenderManager.java

## Přehled

`RenderManager` je rozhraní, které spravuje plánování a provádění úloh vykreslování (renderingu) mapových dlaždic (
tiles). Umožňuje plánovat aktualizace celých map nebo jen konkrétních regionů a ovládat stav rendereru (start/stop).

## Umístění

`de.bluecolored.bluemap.api.RenderManager`

## Metody

### `scheduleMapUpdateTask(BlueMapMap map)`

Naplánuje úlohu pro aktualizaci dané mapy.

- **Parametry:**
    - `map`: Mapa, která se má aktualizovat.
- **Návratová hodnota:** `true`, pokud byla úloha úspěšně naplánována, `false` pokud ne (např. už je naplánována).
- Zkratka pro `scheduleMapUpdateTask(map, false)`.

### `scheduleMapUpdateTask(BlueMapMap map, boolean force)`

Naplánuje úlohu pro aktualizaci dané mapy s možností vynucení vykreslení.

- **Parametry:**
    - `force`: Pokud je `true`, přegenerují se všechny dlaždice, i když nedošlo ke změně.

### `scheduleMapUpdateTask(BlueMapMap map, Collection<Vector2i> regions, boolean force)`

Naplánuje úlohu pro aktualizaci konkrétních regionů mapy.

- **Parametry:**
    - `regions`: Kolekce souřadnic regionů (region-files, 32x32 chunků), které se mají aktualizovat. BlueMap pracuje na
      úrovni regionů, nelze aktualizovat menší jednotky samostatně.

### `scheduleMapPurgeTask(BlueMapMap map)`

Naplánuje úlohu pro vymazání (purge) mapy. Po vymazání se automaticky naplánuje aktualizace, aby se mapa znovu
vygenerovala.

### `renderQueueSize()`

Vrací aktuální počet úloh ve frontě vykreslování.

### `renderThreadCount()`

Vrací počet vláken, která jsou aktuálně vyhrazena pro vykreslování.

### `isRunning()`

Vrací `true`, pokud renderer právě běží.

### `start()`

Spustí renderer, pokud neběží. Použije nakonfigurovaný počet vláken.

### `start(int threadCount)`

Spustí renderer s definovaným počtem vláken.

- `threadCount`: Počet vláken (> 0).

### `stop()`

Zastaví renderer, pokud běží. Probíhající úlohy mohou být přerušeny.
