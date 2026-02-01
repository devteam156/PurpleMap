# Chunk_1_13.java (Formát 1.13 - 1.14)

## Přehled

Implementace chunku pro Minecraft verze 1.13 až 1.14.4. Tento formát zavedl "Flattening" (palety bloků místo ID:Data),
ale biomy byly stále uloženy jako prosté pole 256 integerů na chunk (XZ plocha).

## Umístění

`de.bluecolored.bluemap.core.world.mca.chunk.Chunk_1_13`

## Vnitřní Logika Načítání

1. **Stav chunku:** Kontroluje pole `Status` v NBT. Pokud je `empty`, chunk se považuje za negenerovaný. Světelná data
   jsou přítomna pouze pro stavy `full`, `fullchunk` nebo `postprocessed`.
2. **Sekce:** Prochází pole `Sections`. Každá sekce představuje krychli 16x16x16 bloků. BlueMap je ukládá do pole
   indexovaného podle výšky Y.
3. **Blokové entity:** Převede seznam `TileEntities` na mapu, kde klíčem je hash souřadnic (Y << 8 | X << 4 | Z). To
   umožňuje bleskový přístup k entitám (cedulky, lebky) při renderování bloku.

## Metody a Výpočty

### `getBlockState(int x, int y, int z)`

- **Logika:** Najde sekci podle `y >> 4`. Pokud existuje, deleguje volání na `Section.getBlockState`.

### `getBiome(int x, int y, int z)`

- **Logika:** V této verzi jsou biomy 2D. Index se vypočítá jako `(z & 0xF) << 4 | x & 0xF`.

### `getWorldSurfaceY(int x, int z)`

- **Logika:** Čte z pole `WORLD_SURFACE` (9 bitů na prvek) pomocí `MCAUtil.getValueFromLongStream`.

## Vnitřní třída `Section`

Reprezentuje jednu výškovou vrstvu chunku.

- **`blocks`**: Pole `long[]` obsahující zabalené indexy do palety.
- **`bitsPerBlock`**: Vypočítá se z délky pole `blocks` (počet longů * 64 / 4096).
- **`blockPalette`**: Pole `BlockState[]` (např. 0 -> AIR, 1 -> STONE).
- **`getBlockState(...)`**:
    1. Vypočítá index bloku v sekci: `(y & 0xF) << 8 | (z & 0xF) << 4 | x & 0xF`.
    2. Získá ID z bitového proudu.
    3. Vrátí `BlockState` z palety.