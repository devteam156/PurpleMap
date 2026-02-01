# BlurMaskConfig.java

## Přehled

Speciální typ masky, který neaplikuje geometrický tvar, ale "rozmazává" (graduálně mění průhlednost) okraje existujících
masek.

## Umístění

`de.bluecolored.bluemap.common.config.mask.BlurMaskConfig`

## Atributy

- `size`: Šířka přechodové oblasti v blocích.
- `masks`: `CombinedMask` - Seznam masek, na které se má rozmazání aplikovat.

## Metody

### `createMask()`

- **Logika:**
    - Pokud je `size > 0`, vytvoří instanci `BlurMask` obalující vnořené masky.
    - Pokud je `size <= 0`, vrátí vnořené masky přímo bez rozmazání.