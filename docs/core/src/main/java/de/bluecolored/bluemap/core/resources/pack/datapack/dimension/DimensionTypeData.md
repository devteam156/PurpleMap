# DimensionTypeData.java

## Přehled

`DimensionTypeData` je přepravka (data class) pro deserializaci definice dimenze (`dimension_type`) z JSONu.
Implementuje rozhraní `DimensionType`.

## Umístění

`de.bluecolored.bluemap.core.resources.pack.datapack.dimension.DimensionTypeData`

## Implementovaná Rozhraní

`DimensionType`

## Atributy (z JSONu)

- `natural`: Zda je dimenze přírodní (vliv na kompas atd.).
- `has_skylight`: Zda má nebeské světlo.
- `has_ceiling`: Zda má strop (bedrock, např. Nether).
- `ambient_light`: Úroveň ambientního světla.
- `min_y`, `height`: Výškový rozsah.
- `coordinate_scale`: Měřítko souřadnic (např. 8.0 pro Nether).
