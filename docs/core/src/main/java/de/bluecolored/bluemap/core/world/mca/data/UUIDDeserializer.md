# UUIDDeserializer.java

## Přehled

`UUIDDeserializer` je deserializér pro `java.util.UUID` z NBT dat.

## Umístění

`de.bluecolored.bluemap.core.world.mca.data.UUIDDeserializer`

## Funkcionalita

Podporuje tři různé formáty zápisu UUID v NBT, které se v historii Minecraftu vystřídaly:

1. **String:** `"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"` (nejstarší/textový).
2. **Int Array:** `[I; 1, 2, 3, 4]` (nový formát, 4x 32bit int).
3. **Long Array:** `[L; 1, 2]` (přechodný formát? 2x 64bit long).

Deserializér rozpozná typ tagu a správně ho převede na `UUID`.
