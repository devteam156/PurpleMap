# PolygonMaskConfig.java

## Přehled

Konfiguruje masku ve tvaru obecného polygonu definovaného v rovině XZ, s volitelným omezením výšky (Y).

## Umístění

`de.bluecolored.bluemap.common.config.mask.PolygonMaskConfig`

## Atributy

- `minY`, `maxY`: Rozsah výšky. Výchozí jsou minimální a maximální hodnoty integeru.
- `shape`: Pole `Vector2d[]` - Seznam bodů definujících obvod polygonu.

## Metody

### `createMask()`

- **Logika:**
    1. Ověří, zda `minY <= maxY`.
    2. Ověří, zda má polygon alespoň 3 body.
    3. Vrátí instanci `PolygonMask`.

    - **Algoritmus:** `PolygonMask` interně používá Ray-casting algoritmus pro zjištění, zda bod leží uvnitř polygonu.