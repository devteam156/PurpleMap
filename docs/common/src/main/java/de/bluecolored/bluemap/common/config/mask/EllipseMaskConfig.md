# EllipseMaskConfig.java

## Přehled

Konfiguruje masku ve tvaru elipsy v rovině XZ.

## Umístění

`de.bluecolored.bluemap.common.config.mask.EllipseMaskConfig`

## Atributy

- `centerX`, `centerZ`: Střed elipsy.
- `radiusX`, `radiusZ`: Poloměry v osách X a Z.
- `minY`, `maxY`: Výškový rozsah.

## Metody

### `createMask()`

- **Logika:** Vrátí instanci `EllipseMask`.
    - **Matematika:** Bod `(x, z)` je uvnitř, pokud `(x-cx)^2 / rx^2 + (z-cz)^2 / rz^2 <= 1`.