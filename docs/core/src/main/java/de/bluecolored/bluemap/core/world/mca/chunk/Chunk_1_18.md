# Chunk_1_18.java

## Přehled

`Chunk_1_18` je implementace `MCAChunk` pro formát chunků používaný v Minecraftu 1.18 a novějších (Caves & Cliffs).

## Umístění

`de.bluecolored.bluemap.core.world.mca.chunk.Chunk_1_18`

## Dědičnost

`MCAChunk` -> `Chunk_1_18`

## Změny oproti 1.16

- **Změna výšky světa:** Podporuje záporné Y souřadnice (minY může být např. -64).
- **Nová struktura sekcí:** Sekce (`Section`) nyní obsahují paletu a data nejen pro bloky, ale i pro **biomy**. Biomy
  jsou uloženy v každé sekci zvlášť, nikoliv globálně pro celý chunk.
- **Odstranění globálního pole biomů:** Metoda `getBiome` nyní čte data ze sekce.

## Metody

- `getWorldSurfaceY` / `getOceanFloorY`: Zohledňují `worldMinY` (offset).
- `getBiome`: Získá biom ze sekce odpovídající dané výšce.
