# Chunk_1_15.java

## Přehled

Drobná evoluce formátu 1.13 pro verzi 1.15. Hlavní změnou je zavedení **3D biomů**.

## Umístění

`de.bluecolored.bluemap.core.world.mca.chunk.Chunk_1_15`

## Rozdíly v Logice

### `getBiome(int x, int y, int z)`

Minecraft 1.15 zavedl vzorkování biomů po 4 blocích ve všech osách (4x4x4 bloky na jeden vzorek).

- **Indexace:** Index v poli biomes (které má nyní 1024 prvků pro celý výškový sloupec nebo 64 na sekci) se počítá
  bitovými operacemi: `(y & 0b1100) << 2 | z & 0b1100 | (x & 0b1100) >> 2`.
- **Ošetření rozsahu:** Obsahuje logiku pro posun indexu, pokud by vypočtená hodnota byla mimo pole (např. u modovaných
  světů s jinou výškou).