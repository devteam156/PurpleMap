# PolygonMask.java

## Přehled

`PolygonMask` definuje oblast pomocí 2D polygonu (na rovině XZ) a výškového rozsahu.

## Umístění

`de.bluecolored.bluemap.core.map.mask.PolygonMask`

## Atributy

- `shape`: Tvar (`Shape`), který definuje body polygonu.
- `minY`, `maxY`: Rozsah výšky.

## Metody

### `test(int x, int y, int z)`

Testuje, zda je bod uvnitř polygonu (ray-casting algoritmus) a v rozsahu výšek.

### `testXZ(minX, minZ, maxX, maxZ)`

Testuje průnik obdélníku s polygonem.

- Kontroluje průsečíky hran polygonu s hranami obdélníku.
- Pokud nejsou průsečíky, kontroluje, zda je jeden bod uvnitř druhého.
