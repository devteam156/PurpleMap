# Vector2iDeserializer.java

## Přehled

`Vector2iDeserializer` je deserializér pro `Vector2i` (2D celočíselný vektor) z NBT dat.

## Umístění

`de.bluecolored.bluemap.core.world.mca.data.Vector2iDeserializer`

## Funkcionalita

Načítá `Vector2i` z různých NBT formátů:

- Pole: `[int, int]` (nebo long array)
- List: `[double, double]`
- Compound: `{"x": 1, "y": 2}`
