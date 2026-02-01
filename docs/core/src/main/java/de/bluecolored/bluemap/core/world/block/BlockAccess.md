# BlockAccess.java

## Přehled

`BlockAccess` je rozhraní pro čtení informací o bloku na určité pozici.

## Umístění

`de.bluecolored.bluemap.core.world.block.BlockAccess`

## Metody

### `set(int x, int y, int z)`

Přesune pohled na jiný blok.

### `copy()`

Vytvoří kopii tohoto přístupového objektu (např. pro uložení stavu).

### Gettery

- `getX()`, `getY()`, `getZ()`: Souřadnice.
- `getBlockState()`: Stav bloku (typ, vlastnosti).
- `getLightData()`: Osvětlení.
- `getBiome()`: Biom.
- `getBlockEntity()`: Entita bloku (pokud existuje).
- `getSunLightLevel()`, `getBlockLightLevel()`: Pomocné metody pro získání úrovně světla.
- `getOceanFloorY()`: Výška dna oceánu na dané souřadnici X, Z.
