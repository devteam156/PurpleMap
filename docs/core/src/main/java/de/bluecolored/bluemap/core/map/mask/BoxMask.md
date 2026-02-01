# BoxMask.java

## Přehled

`BoxMask` je nejjednodušší typ masky, který definuje kvádr (osově zarovnaný bounding box - AABB).

## Umístění

`de.bluecolored.bluemap.core.map.mask.BoxMask`

## Atributy

- `min`, `max`: Vektory definující protilehlé rohy kvádru.

## Metody

### `test(int x, int y, int z)`

Vrátí `true`, pokud jsou souřadnice uvnitř kvádru.

### `test(minX, minY, minZ, maxX, maxY, maxZ)`

Testuje průnik s jiným AABB.

- `TRUE`: Celá testovaná oblast je uvnitř masky.
- `FALSE`: Celá testovaná oblast je mimo masku.
- `UNDEFINED`: Částečný průnik.
