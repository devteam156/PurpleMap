# CombinedRenderTask.java

## Přehled

`CombinedRenderTask` je generická implementace `RenderTask`, která slouží jako kontejner pro sekvenci jiných úloh.
Umožňuje seskupit logicky související akce (např. renderování mnoha regionů a následné uložení) do jedné entity ve
frontě `RenderManager`u.

## Umístění

`de.bluecolored.bluemap.common.rendermanager.CombinedRenderTask`

## Balíček

`de.bluecolored.bluemap.common.rendermanager`

## Atributy

- `description`: Textový popis celého balíku úloh.
- `tasks`: Neměnný seznam (`List<T>`) vnořených úloh.
- `currentTaskIndex`: Index právě prováděné vnořené úlohy.

## Vnitřní Logika a Metody

### `doWork()`

Metoda postupně deleguje práci na vnořené úlohy:

1. Získá úlohu na indexu `currentTaskIndex`.
2. Zkontroluje, zda má úloha ještě práci (`hasMoreWork()`).
3. Pokud ne, inkrementuje `currentTaskIndex` (přesune se na další úlohu).
4. Pokud ano, zavolá `task.doWork()`.

- **Poznámka:** Volání je thread-safe díky `synchronized` bloku při kontrole indexu a stavu. Samotná práce (
  `task.doWork()`) ale běží mimo zámek, což umožňuje paralelismus, pokud vnořená úloha (např. `WorldRegionRenderTask`)
  paralelismus podporuje.

### `estimateProgress()`

Vypočítá celkový postup jako kombinaci hotových úloh a rozpracované úlohy:

- `(index + rozpracovanost_aktualni_ulohy) / celkovy_pocet_uloh`.
- Vrací hodnotu 0.0 až 1.0.

### `cancel()`

Zavolá metodu `cancel()` na **všech** vnořených úlohách bez ohledu na to, zda jsou rozpracované nebo teprve čekají.

### `contains(RenderTask task)`

Implementuje rekurzivní vyhledávání úloh. Tato úloha "obsahuje" jinou, pokud:

- Je to přímo ona.
- Je to jiný `CombinedRenderTask` a všechny jeho podúlohy jsou obsaženy zde.
- Některá z jejích podúloh obsahuje hledanou úlohu.
- Tato logika je klíčová pro deduplikaci ve frontě `RenderManager`u.
