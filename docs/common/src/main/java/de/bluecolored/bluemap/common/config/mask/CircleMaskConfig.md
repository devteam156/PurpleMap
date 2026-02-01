# CircleMaskConfig.java

## Přehled

Zjednodušená verze elipsy, kde jsou oba poloměry shodné.

## Umístění

`de.bluecolored.bluemap.common.config.mask.CircleMaskConfig`

## Atributy

- `centerX`, `centerZ`: Střed kruhu.
- `radius`: Poloměr.
- `minY`, `maxY`: Výškový rozsah.

## Metody

### `createMask()`

- **Logika:** Vytvoří `EllipseMask`, kde `radiusX` i `radiusZ` jsou nastaveny na hodnotu `radius`.