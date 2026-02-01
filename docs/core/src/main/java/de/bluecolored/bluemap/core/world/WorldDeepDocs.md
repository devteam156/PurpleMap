# World Root Classes & Interfaces

## Přehled

Balíček `de.bluecolored.bluemap.core.world` definuje abstraktní model Minecraft světa. Jádro BlueMap pracuje s těmito
rozhraními, což umožňuje nezávislost na konkrétním formátu uložení (i když MCA je primární).

---

# World.java (Rozhraní)

## Přehled

Reprezentuje jeden herní svět nebo dimenzi. Implementace musí být **vláknově bezpečná**.

## Klíčové Metody

- `getId()`: Unikátní řetězec identifikující svět (vytvořen z cesty a dimenze).
- `getChunk(x, z)`: Vrátí objekt `Chunk` pro dané souřadnice chunku.
- `getRegion(x, z)`: Vrátí objekt `Region` (skupina chunků).
- `listRegions()`: Prohledá soubory a vrátí seznam dostupných regionů.
- `preloadRegionChunks(...)`: Masivní optimalizace. Načte vybrané chunky z regionu do paměti najednou.
- `invalidateChunkCache()`: Vymaže cache, vynutí znovunačtení dat z disku.
- `iterateEntities(...)`: Projde všechny entity v zadané oblasti a předá je consumeru.

---

# Chunk.java (Rozhraní)

## Přehled

Reprezentuje vertikální sloupec světa (16x16 bloků).

## Klíčové Metody

- `isGenerated()`: Zda chunk obsahuje reálná data (není prázdný).
- `hasLightData()`: Zda má chunk vypočtené osvětlení.
- `getBlockState(x, y, z)`: Vrátí stav bloku na lokálních souřadnicích.
- `getLightData(...)`: Vrátí úroveň světla (obloha + bloky).
- `getBiome(...)`: Vrátí biom na dané pozici.
- `getWorldSurfaceY(x, z)`: Vrátí nejvyšší pevný blok (z výškové mapy).
- `getBlockEntity(...)`: Získá doplňující data bloku na pozici.

---

# BlockState.java

## Přehled

Neměnná (immutable) a thread-safe třída reprezentující konkrétní typ bloku a jeho vlastnosti (např.
`minecraft:oak_stairs[facing=north]`).

## Atributy

- `id`: `Key` - Identifikátor bloku.
- `properties`: `Map<String, String>` - Vlastnosti (states).
- `isAir`, `isWater`, `isWaterlogged`: Optimalizované boolean příznaky pro rychlé rozhodování při renderování.

## Funkcionalita a Logika

- **Interning:** Vlastnosti bloku jsou při parsování internovány pro úsporu paměti.
- **`fromString(String)`**: Obsahuje regulární výraz pro parsování Minecraft zápisu bloků.
    - **Pattern:** `^(.+?)(?:\[(.*)])?$` -> Rozdělí řetězec na ID a část v hranatých závorkách.
- **Rychlý přístup k datům:** Metody `getLiquidLevel()` a `getRedstonePower()` parsují hodnoty z mapy vlastností jen v
  případě potřeby a výsledek si cachují.

---

# BlockProperties.java

## Přehled

Přepravka pro technické vlastnosti bloku, které ovlivňují proces renderování geometrie.

## Atributy (Vše typu `Tristate`)

- `culling`: Zda blok schovává stěny sousedních bloků.
- `occluding`: Zda je blok neprůhledný (zastiňuje světlo).
- `alwaysWaterlogged`: Zda má být blok vždy vykreslen jako pod vodou.
- `randomOffset`: Zda se má model bloku náhodně posunout (např. tráva, květiny).
- `cullingIdentical`: Zda mají být skryty stěny mezi dvěma identickými bloky (např. sklo).

---

# DimensionType.java (Rozhraní)

## Přehled

Definuje fyzikální a geometrické parametry dimenze.

## Předdefinované Typy

- `OVERWORLD`: Výška 384, minY -64, koordináty 1:1.
- `NETHER`: Výška 256, má strop, koordináty 8:1 (vzdálenost v Netheru se násobí 8).
- `END`: Výška 256, pevný čas (noc).

---

# Ostatní Třídy

### `LightData.java`

- Jednoduchý kontejner pro dvě hodnoty: `skyLight` a `blockLight` (0-15).

### `BlockEntity.java` (Rozhraní)

- Základní kontrakt pro doplňující data bloku (ID a souřadnice).
