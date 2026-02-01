# MCAChunkLoader.java

## Přehled

`MCAChunkLoader` je implementace rozhraní `ChunkLoader` pro formát MCA. Jeho hlavní zodpovědností je detekovat verzi dat
v NBT struktuře chunku a na základě toho vytvořit instanci správné verze `MCAChunk` (např. `Chunk_1_18`).

## Umístění

`de.bluecolored.bluemap.core.world.mca.chunk.MCAChunkLoader`

## Balíček

`de.bluecolored.bluemap.core.world.mca.chunk`

## Atributy

### `world`

- **Typ:** `MCAWorld`
- **Popis:** Svět, do kterého načítané chunky patří. Slouží k získání informací o datapacku a typu dimenze.

### `CHUNK_VERSION_LOADERS`

- **Typ:** `List<ChunkVersionLoader<?>>`
- **Popis:** Statický, seřazený seznam definic verzí chunků. Seřazeno od nejnovější po nejstarší.
    - 1.18+: od verze 2844
    - 1.16+: od verze 2500
    - 1.15+: od verze 2200
    - 1.13+: od verze 0

### `lastUsedLoader`

- **Typ:** `ChunkVersionLoader`
- **Popis:** Instance loaderu, který byl použit naposledy. Slouží jako optimalizace (heuristika), protože je velmi
  pravděpodobné, že sousední chunky budou mít stejnou verzi.

## Vnitřní Logika a Metody

### `load(byte[] data, int offset, int length, Compression compression)`

Hlavní metoda pro načtení chunku z binárních dat.

1. **Příprava:** Vytvoří `ByteArrayInputStream` a označí si začátek (`mark`).
2. **První pokus (Optimalizovaný):**
    - Použije `lastUsedLoader` k pokusu o načtení dat.
    - Data dekomprimuje pomocí zadané komprese (GZIP/Zlib).
    - Deserializuje NBT do příslušné datové třídy (např. `Chunk_1_18.Data`).
3. **Kontrola verze:**
    - Získá `DataVersion` z právě načtených dat.
    - Pomocí `findBestLoaderForVersion` zjistí, který loader je pro tuto verzi skutečně nejvhodnější.
4. **Druhý pokus (V případě neshody):**
    - Pokud se verze neshoduje s předpokládanou (např. načítali jsme 1.18, ale v NBT je 1.16), resetuje stream na
      začátek.
    - Znovu dekomprimuje a načte data pomocí správného loaderu.
    - Aktualizuje `lastUsedLoader`.
5. **Výsledek:** Vrátí instanci `MCAChunk`.

### `findBestLoaderForVersion(int version)`

Prochází seznam `CHUNK_VERSION_LOADERS` a vrátí první, jehož minimální podporovaná verze je menší nebo rovna zadané
verzi.

## Vnitřní třída `ChunkVersionLoader`

Zapouzdřuje logiku pro jednu konkrétní verzi chunku.

- **`dataType`**: Třída s NBT strukturou (např. `Chunk_1_18.Data.class`).
- **`constructor`**: Odkaz na konstruktor (funkci), která vytvoří instanci `MCAChunk`.
- **`load(...)`**:
    - Volá `BlueNBT` pro načtení streamu do `dataType`.
    - Volá konstruktor a vrací objekt.
    - Pokud parsování selže, vyhodí `IOException` s popisem, u jakého typu dat chyba nastala.