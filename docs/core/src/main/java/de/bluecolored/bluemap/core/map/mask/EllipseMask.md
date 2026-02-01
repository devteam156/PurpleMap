# EllipseMask.java

## Přehled

`EllipseMask` je maska, která definuje oblast ve tvaru elipsy (nebo kruhu) s omezenou výškou.

## Umístění

`de.bluecolored.bluemap.core.map.mask.EllipseMask`

## Atributy

- `center`: Střed elipsy (`Vector2d`).
- `radiusSquaredX`, `radiusSquaredZ`: Druhé mocniny poloměrů (pro efektivnější výpočty).
- `minY`, `maxY`: Rozsah výšky.

## Metody

### `test(int x, int y, int z)`

Vrátí `true`, pokud je bod uvnitř elipsy a v povoleném rozsahu výšek.

### `test(minX, minY, minZ, maxX, maxY, maxZ)`

Testuje průnik oblasti (AABB) s maskou.

- Používá efektivní kontrolu: pokud je obdélník plně uvnitř kruhu, vrátí `TRUE`. Pokud je nejbližší bod obdélníku mimo
  kruh, vrátí `FALSE`. Jinak `UNDEFINED`.
