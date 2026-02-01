# Vector3dDeserializer.java

## Přehled

`Vector3dDeserializer` je deserializér pro `Vector3d` (3D vektor s `double` souřadnicemi).

## Umístění

`de.bluecolored.bluemap.core.world.mca.data.Vector3dDeserializer`

## Funkcionalita

Načítá `Vector3d` z různých NBT formátů:

- Pole: `[long, long, long]`
- List: `[double, double, double]`
- Compound: `{"x": 1.0, "y": 2.0, "z": 3.0}`
