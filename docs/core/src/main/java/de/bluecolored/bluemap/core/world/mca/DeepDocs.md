# MCA Format Deep Docs (Anvil System)

## Přehled

Balíček `de.bluecolored.bluemap.core.world.mca` implementuje specifikaci formátu Anvil, který Minecraft používá k
ukládání světů od verze 1.2. BlueMap čte přímo binární soubory `.mca` a extrahuje z nich data o blocích a entitách.

---

# MCARegion.java (Binární Region Parser)

## Přehled

Zodpovídá za čtení jednoho souboru `.mca` (např. `r.0.0.mca`). Soubor obsahuje data pro 32x32 chunků (celkem 1024).

## Vnitřní Logika: Struktura Regionu

Soubor je rozdělen do sektorů po 4096 bajtech.

1. **Tabulka umístění (Location Table):** Prvních 4096 bajtů. Každý chunk má 4bajty:
    - První 3 bajty: Offset sektoru v souboru.
    -
        4. bajt: Počet sektorů, které chunk zabírá.
2. **Tabulka časových razítek (Timestamp Table):** Dalších 4096 bajtů. Obsahuje čas poslední změny každého chunku.
   BlueMap tyto hashy používá k detekci změn pro inkrementální renderování.
3. **Dekomprese chunku:**
    - Každý chunk začíná 4bajty délky a 1bajtem typu komprese.
    - BlueMap podporuje: 1 (GZIP), 2 (Zlib/Deflate), 4 (LZ4).
    - Metoda `loadChunk` nejdříve identifikuje kompresi, odstraní hlavičku a předá zbytek bajtů do `MCAChunkLoader`.

---

# MCAWorld.java (Světový orchestrátor)

## Přehled

Implementace rozhraní `World` pro formát MCA. Propojuje fyzické soubory s logikou Minecraftu.

## Vnitřní Logika a Metody

- **`blockChunkGrid` & `entityChunkGrid`**: MCAWorld udržuje dvě oddělené mřížky. Jedna čte soubory ze složky
  `region/` (bloky), druhá ze složky `entities/` (entity jako truhly, cedulky – od verze 1.17).
- **`resolveDimensionFolder`**: Obsahuje logiku pro vyhledání dat dimenzí. Např. Nether je v `DIM-1`, End v `DIM1`, a
  modované dimenze v `dimensions/namespace/value`.
- **`load(...)`**: Nejdříve načte a rozbalí `level.dat`, ze kterého získá název světa a globální nastavení generátoru.

---

# MCAUtil.java (Bitové operace)

## Přehled

Knihovna nízkoúrovňových utilit pro práci s bitově balenými daty Minecraftu.

## Klíčové Metody

- **`getValueFromLongStream(data, index, bits)`**: Nejdůležitější metoda pro moderní Minecraft (1.13+).
    - **Problém:** Minecraft balí data (např. indexy bloků) do pole `long[]` tak, že jedna hodnota může být rozdělená
      mezi dva sousední `long` prvky.
    - **Logika:** Metoda vypočítá přesný bitový offset, načte příslušné `long` hodnoty, provede bitové posuny a spojení
      pomocí masky, aby vrátila čisté číslo.
- **`getByteHalf`**: Rychlá extrakce nibbles (4 bity) z bajtu (používá se pro světelná data).
- **`ceilLog2`**: Vypočítá potřebný počet bitů pro uložení čísla (používá se pro výpočet velikosti palet).

---

# BlueNBT integrace

BlueMap používá pro parsování NBT vlastní vysoce výkonnou knihovnu **BlueNBT**. `MCAUtil` a `MCAWorld` do ní registrují
specifické deserializéry pro Minecraft typy (BlockState, UUID, Vectors), což umožňuje převádět NBT tagy přímo na Java
objekty bez mezikroku s mapami (pro výkon).
