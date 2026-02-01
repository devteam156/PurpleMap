# Block.java

## Přehled

`Block` je implementace `BlockAccess`, která reprezentuje jeden konkrétní blok ve světě. Slouží jako kurzor, který se
posouvá po světě (pomocí `set`), čímž se minimalizuje vytváření nových objektů při iteraci.

## Umístění

`de.bluecolored.bluemap.core.world.block.Block`

## Implementovaná Rozhraní

`BlockAccess`

## Atributy

- `world`: Svět, ve kterém se blok nachází.
- `x, y, z`: Souřadnice bloku.
- `chunk`: Cachovaný odkaz na chunk (resetuje se při změně X nebo Z).
- `blockState`: Cachovaný stav bloku.
- `lightData`: Cachovaná data o světle.
- `biome`: Cachovaný biom.
- `blockEntity`: Cachovaná entita bloku.

## Metody

### `set(int x, int y, int z)`

Přesune kurzor na novou pozici. Vymaže cachovaná data pro tuto pozici (kromě chunku, pokud se nezměnil).

### `getChunk()`

Získá chunk pro aktuální pozici (pokud není načten).

### `getBlockState()`, `getLightData()`, `getBiome()`, `getBlockEntity()`

Získá data pro aktuální pozici z chunku (lazy loading).
