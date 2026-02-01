# Chunk_1_16.java (Formát 1.16 - 1.17)

## Přehled

Implementace pro verze 1.16 a 1.17. Změnil se způsob uložení výškových map a vnitřní struktura NBT (např. biomy jsou
nyní typu `int[]` místo `byte[]`).

## Umístění

`de.bluecolored.bluemap.core.world.mca.chunk.Chunk_1_16`

## Klíčové změny a logika

### Výškové mapy (Heightmaps)

Od 1.16 se výškové mapy neukládají jako fixní pole, ale jsou "bit-packed" podle výšky světa.

- **Výpočet bitů:** `bitsPerHeightmapElement = ceilLog2(worldHeight + 1)`. Např. pro výšku 256 je to 9 bitů.
- **Přístup:** Používá třídu `PackedIntArrayAccess` pro rychlé čtení hodnot z `long[]`.

### Sekce a Bloky

Bloky jsou v sekcích uloženy stejně jako v 1.13, ale BlueMap zde začíná využívat `PackedIntArrayAccess` místo ručního
volání `getValueFromLongStream` pro každou dlaždici, což zpřehledňuje kód.

### Světlo (LightData)

- **Logika:** Světlo je uloženo v polích `BlockLight` a `SkyLight` jako 4bitové hodnoty (nibbles).
- **Indexace:** Jeden byte obsahuje světlo pro dva bloky.
    - Index v poli bytů: `blockByteIndex >> 1`.
    - Která polovina (nibble) se použije, určuje poslední bit indexu bloku (`blockByteIndex & 0x1`).