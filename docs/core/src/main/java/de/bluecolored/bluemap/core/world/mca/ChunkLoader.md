# ChunkLoader.java

## Přehled

`ChunkLoader` je rozhraní pro načítání chunků z binárních dat.

## Umístění

`de.bluecolored.bluemap.core.world.mca.ChunkLoader`

## Metody

### `load(...)`

Načte chunk z pole bytů. Přijímá offset, délku a typ komprese.

### `emptyChunk()`

Vrátí instanci prázdného chunku (pro chybějící data).

### `erroredChunk()`

Vrátí instanci chybového chunku (pro poškozená data).