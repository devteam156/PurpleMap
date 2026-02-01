# Vector2fDeserializer.java

## Přehled

`Vector2fDeserializer` je deserializér pro `Vector2f` z NBT dat.

## Umístění

`de.bluecolored.bluemap.core.world.mca.data.Vector2fDeserializer`

## Funkcionalita

Podporuje načítání vektoru z různých NBT struktur:

- **Pole:** `[float, float]` (nebo int/long pole).
- **List:** `[float, float]`.
- **Compound:** `{"x": 1.0, "y": 2.0}` nebo `{"yaw": 90.0, "pitch": 0.0}` (pro rotace entit).
