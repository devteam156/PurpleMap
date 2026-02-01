# World.java

## Přehled

`World` je rozhraní reprezentující svět (dimenzi) na serveru. Poskytuje přístup k datům světa, jako jsou chunky, bloky a
regiony.

## Umístění

`de.bluecolored.bluemap.core.world.World`

## Metody

### `getId()`

Vrací unikátní ID světa.

### `getName()`

Vrací zobrazované jméno světa.

### `getDimensionType()`

Vrací typ dimenze (Overworld, Nether, End...).

### `getChunkGrid()`, `getRegionGrid()`

Vrací mřížky definující rozložení chunků a regionů.

### `getChunk(int x, int z)`

Vrací chunk na daných souřadnicích chunků.

### `getChunkAtBlock(int x, int z)`

Vrací chunk obsahující danou pozici bloku.

### `getRegion(int x, int z)`

Vrací region na daných souřadnicích regionů.

### `listRegions()`

Vrací seznam souřadnic všech regionů ve světě.

### `createRegionWatchService()`

Vytvoří službu pro sledování změn v regionech (pokud je to podporováno).

### `preloadRegionChunks(int x, int z, Predicate<Vector2i> chunkFilter)`

Načte chunky z regionu do cache.

### `invalidateChunkCache()`

Vymaže cache chunků.

### `iterateEntities(...)`

Iteruje přes všechny entity v zadané oblasti.
