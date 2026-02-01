# Chunk_1_18.java (Formát 1.18+)

## Přehled

Aktuální moderní formát Minecraftu (od verze 1.18). Zavedl variabilní výšku světa (včetně záporných souřadnic Y) a
kompletně změnil uložení biomů – ty jsou nyní také paletizované a bitově zabalené v každé sekci zvlášť.

## Umístění

`de.bluecolored.bluemap.core.world.mca.chunk.Chunk_1_18`

## Hlavní technické inovace

### Variabilní Y (Vertical Expansion)

- `worldMinY`: Načítá se z typu dimenze (např. -64 pro Overworld).
- **Korekce výšky:** Při čtení výškových map se k hodnotě z NBT přičítá `worldMinY`, aby se získala reálná souřadnice
  bloku.

### Paletizované Biomy v Sekcích

V předchozích verzích byly biomy v jednom velkém poli pro celý sloupec (chunk). Od 1.18 má každá sekce (16x16x16) svou
vlastní paletu biomů.

- **Logika:** Pokud je v sekci jen jeden biom, paleta má velikost 1 a bitové pole dat chybí (všechny bloky v sekci mají
  tento biom).
- **Indexace:** Používá 3D vzorkování (4x4x4 bloky). Index se počítá jako v 1.15, ale výsledek se čte z
  `PackedIntArrayAccess` biometrické palety dané sekce.

## Vnitřní třída `Section`

Výrazně složitější než u předchozích verzí:

- **`blockPalette`** & **`blocks`**: Standardní uložení bloků.
- **`biomePalette`** & **`biomes`**: Nový systém pro biomy.
- **`getBlockState(...)`**: Stejná logika jako dříve.
- **`getBiome(...)`**:
    1. Pokud má paleta 1 prvek, vrátí ho hned (optimalizace).
    2. Jinak vypočítá index vzorku (4x4x4) a získá ID biomu z bitového pole `biomes`.
    3. Vrátí biom z palety sekce.
- **`getLightData(...)`**: Zůstává stejné jako v 1.16.

## NBT DTO Struktura

Třída obsahuje velmi podrobnou hierarchii vnitřních tříd (`Data`, `SectionData`, `BlockStatesData`, `BiomesData`), které
přesně kopírují strukturu moderního Minecraft NBT formátu pro rychlou deserializaci pomocí BlueNBT.
