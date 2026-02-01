# Chunk.java

## Přehled

`Chunk` je rozhraní reprezentující jeden chunk ve světě (sloupec 16x16 bloků).

## Umístění

`de.bluecolored.bluemap.core.world.Chunk`

## Konstanty

- `EMPTY_CHUNK`: Prázdný chunk (vzduch).
- `ERRORED_CHUNK`: Chunk, který se nepodařilo načíst.

## Metody

### `isGenerated()`

Zda je chunk plně vygenerován (status `full` nebo podobný).

### `hasLightData()`

Zda chunk obsahuje data o osvětlení.

### `getInhabitedTime()`

Jak dlouho byl chunk obýván hráči (v tickech).

### `getBlockState(int x, int y, int z)`

Vrátí stav bloku na daných souřadnicích.

### `getLightData(int x, int y, int z, LightData target)`

Zapíše data o osvětlení (sky light, block light) do cílového objektu.

### `getBiome(int x, int y, int z)`

Vrátí biom na daných souřadnicích.

### `getMaxY(...)` / `getMinY(...)`

Rozsah výšek v chunku.

### `getBlockEntity(...)`

Vrátí BlockEntity na dané pozici (nebo null).
