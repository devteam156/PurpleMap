# Lowres Map System

## Přehled

Balíček `de.bluecolored.bluemap.core.map.lowres` spravuje hierarchii 2D dlaždic (obrázků PNG). Tyto dlaždice se generují
automaticky během 3D renderování a rekurzivně se zmenšují do dalších úrovní (LOD - Level of Detail).

---

# LowresTile.java

## Přehled

Reprezentuje jeden fyzický obrázek dlaždice na disku.

## Struktura Dat (PNG Encoding)

Každá lowres dlaždice je PNG obrázek, který má **dvojnásobnou výšku** oproti své šířce. BlueMap do něj ukládá dva typy
dat:

1. **Horní polovina:** Barva (RGBA). To, co uživatel vidí na mapě.
2. **Dolní polovina:** Metadata (Výška a Světlo).
    - **Červený kanál:** Úroveň světla z bloků (0-15).
    - **Modrý + Zelený kanál:** Nadmořská výška (Y souřadnice) uložená jako 16bitový integer.
    - Tato data používá webový viewer pro dynamické stínování a zobrazování souřadnic.

## Vnitřní Logika

- **Bezešvé okraje:** Každá dlaždice má ve skutečnosti rozměr `size + 1`. Tento extra pixel na okraji slouží k tomu, aby
  na sebe dlaždice plynule navazovaly bez černých linek.
- **Thread-Safety:** Používá `ReentrantReadWriteLock` pro ochranu `BufferedImage` při zápisu pixelů.

---

# LowresLayer.java

## Přehled

Reprezentuje jednu celou úroveň přiblížení (např. LOD 1).

## Vnitřní Logika: Rekurzivní zmenšování

Toto je srdce algoritmu. Když se změní pixel v LOD 1, tato vrstva vypočítá průměrnou barvu okolí a pošle ji do LOD 2.

1. **`set(...)`**: Zapíše barvu do dlaždice v aktuální vrstvě. Pokud se jedná o pixel na okraji (0,0), zapíše ho i do
   sousedních dlaždic (pro bezešvost).
2. **`saveTile(...)`**:
    - Nejdříve uloží PNG na disk.
    - Poté vypočítá **Downsampling**: Pro každou skupinu pixelů (danou `lodFactor`, např. 2x2) vypočítá průměrnou barvu,
      průměrnou výšku a průměrné světlo.
    - Tyto průměrné hodnoty pošle metodou `nextLayer.set(...)` do další úrovně zmenšení.
3. **Cache:** Používá kombinaci `weakValues` (pro objekty, které se právě používají) a `softValues` (pro LRU cache v
   paměti).

---

# LowresTileManager.java

## Přehled

Orchestrátor celého lowres systému. Implementuje `TileMetaConsumer`.

## Vnitřní Logika

- **Inicializace:** Vytvoří pole `LowresLayer` objektů. Jsou řetězeny za sebou: `LOD 1 -> LOD 2 -> LOD 3 ...`.
- **`set(x, z, color, height, blockLight)`**: Tato metoda je volána hires rendererem pro každý vyrenderovaný blok.
    - Převede absolutní souřadnice bloku na souřadnice dlaždice a lokální pixel.
    - Předá data první vrstvě (`layers[0]`).
- **`save()`**: Postupně zavolá uložení všech vrstev.
