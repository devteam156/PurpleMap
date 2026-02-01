# MapUpdateTask.java

## Přehled

`MapUpdateTask` je konkrétní implementace `CombinedRenderTask`, která reprezentuje proces aktualizace jedné mapy. Skládá
se ze seznamu úloh pro jednotlivé regiony a závěrečného uložení.

## Umístění

`de.bluecolored.bluemap.common.rendermanager.MapUpdateTask`

## Balíček

`de.bluecolored.bluemap.common.rendermanager`

## Dědičnost

`CombinedRenderTask<RenderTask>` -> `MapUpdateTask`
**Implementuje:** `MapRenderTask`

## Konstruktory

### `MapUpdateTask(BmMap map, Collection<Vector2i> regions, TileUpdateStrategy force)`

Hlavní konstruktor používaný pro plánování aktualizace specifických regionů.
**Logika:**

1. Vytvoří stream z předaných souřadnic regionů.
2. Pro každý region vytvoří instanci `WorldRegionRenderTask`.
3. Na konec seznamu přidá jednu instanci `MapSaveTask` (aby se zajistilo uložení mapy po všech regionech).
4. Převede stream na list a zavolá super-konstruktor.

## Atributy

- `map`: Instance `BmMap`, které se tato aktualizace týká. (Dostupná přes getter).

## Metody

Třída přebírá veškerou funkčnost z `CombinedRenderTask`. Slouží především jako typově definovaný obal pro snazší
identifikaci úloh v `RenderManager`u.
