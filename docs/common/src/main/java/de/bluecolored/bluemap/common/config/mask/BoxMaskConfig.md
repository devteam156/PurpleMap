# BoxMaskConfig.java

## Přehled

Konfiguruje masku ve tvaru 3D kvádru (AABB - Axis Aligned Bounding Box).

## Umístění

`de.bluecolored.bluemap.common.config.mask.BoxMaskConfig`

## Atributy

- `minX`, `minY`, `minZ`: Minimální souřadnice rohu.
- `maxX`, `maxY`, `maxZ`: Maximální souřadnice protilehlého rohu.

## Metody

### `createMask()`

- **Logika:** Vrátí instanci `BoxMask`.
    - **Matematika:** Bod je uvnitř, pokud platí `minX <= x <= maxX` AND `minY <= y <= maxY` AND `minZ <= z <= maxZ`.
    - Pokud jsou min > max, vyhodí výjimku.
    - Výchozí hodnoty jsou nastaveny na nekonečno (MIN/MAX INT), takže prázdný box maskuje celý svět (pokud není
      omezen).