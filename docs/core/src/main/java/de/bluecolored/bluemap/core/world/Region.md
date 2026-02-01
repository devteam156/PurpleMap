# Region.java

## Přehled

`Region` je rozhraní reprezentující oblast světa, která obsahuje chunky (typicky soubor `.mca`).

## Umístění

`de.bluecolored.bluemap.core.world.Region`

## Generika

- `<T>`: Typ chunku.

## Metody

### `iterateAllChunks(ChunkConsumer<T> consumer)`

Iteruje přes všechny chunky v regionu. Nejprve zavolá `consumer.filter` a pouze pokud vrátí true, načte chunk a zavolá
`consumer.accept`.

### `loadChunk(int chunkX, int chunkZ)`

Načte konkrétní chunk. Výchozí implementace používá `iterateAllChunks` s filtrem na jeden chunk (což je neefektivní,
implementace by to měly přepsat).

### `emptyChunk()`

Vrátí instanci prázdného chunku.
