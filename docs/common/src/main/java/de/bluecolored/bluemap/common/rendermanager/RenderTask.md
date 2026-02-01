# RenderTask.java

## Přehled

`RenderTask` je základní rozhraní pro všechny jednotky práce, které lze vložit do `RenderManager`u. Definuje kontrakt
pro asynchronní, přerušitelné a monitorovatelné úlohy.

## Umístění

`de.bluecolored.bluemap.common.rendermanager.RenderTask`

## Metody (Kontrakt)

### `doWork()`

- **Význam:** Vykoná část práce.
- **Logika:** Tato metoda by měla provést malý, ale významný kus práce (např. vyrenderovat jednu dlaždici) a rychle se
  vrátit. `RenderManager` ji volá opakovaně v cyklu.

### `hasMoreWork()`

- **Význam:** Indikuje, zda má úloha ještě co dělat.
- **Logika:** Pokud vrátí `false`, manažer úlohu odstraní z fronty.

### `estimateProgress()`

- **Význam:** Odhad postupu (0.0 až 1.0).
- **Logika:** Slouží pro UI a odhad času.

### `cancel()`

- **Význam:** Žádost o předčasné ukončení.
- **Logika:** Úloha by si měla tento příznak uložit a v příštím volání `doWork()` (nebo dříve) práci ukončit a nastavit
  `hasMoreWork` na `false`.

### `contains(RenderTask task)`

- **Význam:** Logika pro deduplikaci úloh ve frontě.
- **Logika:** Umožňuje jedné úloze říct, že v sobě zahrnuje práci jiné úlohy.

### `getDescription()`

- **Význam:** Krátký lidsky čitelný popis (např. "rendering region 1,2").
