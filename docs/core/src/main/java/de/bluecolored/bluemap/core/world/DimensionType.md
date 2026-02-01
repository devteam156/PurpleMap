# DimensionType.java

## Přehled

`DimensionType` definuje vlastnosti dimenze (světa), jako je Overworld, Nether nebo End.

## Umístění

`de.bluecolored.bluemap.core.world.DimensionType`

## Konstanty (Předdefinované typy)

- `OVERWORLD`: Standardní svět (y -64 až 384).
- `OVERWORLD_CAVES`: Jeskynní svět (má strop).
- `NETHER`: Nether (y 0 až 256, strop, ambient light).
- `END`: The End.

## Metody (Vlastnosti)

- `isNatural()`: Přírodní dimenze.
- `hasSkylight()`: Má nebeské světlo.
- `hasCeiling()`: Má strop (bedrock).
- `getAmbientLight()`: Úroveň okolního světla.
- `getMinY()`, `getHeight()`: Rozsah výšek.
- `getCoordinateScale()`: Měřítko souřadnic (např. 8.0 pro Nether travel).
