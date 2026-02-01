# Vector3iDeserializer.java

## Přehled

`Vector3iDeserializer` je deserializér pro `Vector3i` (3D celočíselný vektor).

## Umístění

`de.bluecolored.bluemap.core.world.mca.data.Vector3iDeserializer`

## Funkcionalita

Načítá `Vector3i` z různých NBT formátů:

- Pole: `[long, long, long]`
- List: `[int, int, int]`
- Compound: `{"x": 1, "y": 2, "z": 3}`
