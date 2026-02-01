# Frontend Tile Streaming System

## Přehled

Balíček `de.bluecolored.bluemap.common.webapp.src.js.map` spravuje životní cyklus dlaždic v prohlížeči. Používá
strategii "Load-on-Demand", kdy se data načítají pouze pro oblast, kterou uživatel právě vidí.

---

# Map.js

## Přehled

Reprezentuje jednu mapu v prohlížeči. Je to reaktivní objekt (Vue 3), který drží konfiguraci a reference na manažery
dlaždic.

## Vnitřní Logika a Načítání

Metoda `load()` provádí inicializaci mapy:

1. **Settings:** Načte `settings.json` a nastaví parametry jako počáteční pozici, barvy oblohy a rozsahy LOD.
2. **Textures:** Načte `textures.json`. Pro každou texturu vytvoří `Three.Texture` a nastaví filtry (Nearest pro
   Minecraft vzhled).
3. **Hires Materials:** Vytvoří pole materiálů (`ShaderMaterial`). Každá textura v galerii má svůj vlastní unikátní
   materiál. To je nezbytné pro správné renderování hires modelů.
4. **LOD Managers:** Vytvoří pole `TileManager`ů pro hires vrstvu a pro každou lowres LOD vrstvu.

---

# TileManager.js

## Přehled

Zodpovídá za správu viditelných dlaždic v rámci jedné vrstvy (např. Hires nebo LOD 1).

## Vnitřní Logika: Spirálové načítání

- **`loadAroundTile(x, z, radiusX, radiusZ)`**: Hlavní metoda volaná při pohybu kamery.
    1. **Odstranění:** Nejdříve uvolní z paměti dlaždice, které jsou mimo viditelný dosah (`removeFarTiles`).
    2. **Výpočet Spirály:** Metoda `loadNextTile` prochází souřadnice kolem středu v rostoucí spirále. To zajišťuje, že
       se nejdříve načtou dlaždice přímo před kamerou.
    3. **Prioritizace:** Pokud se zrovna načítá mnoho dlaždic (více než 8 současně), manažer zpomalí plánování dalších,
       aby nezahltil síť a CPU.
- **`tileMap`**: Speciální pomocný objekt (2D pole), který si pamatuje, které dlaždice jsou v okolí kamery načteny. Tato
  data se předávají shaderům jako textura, aby věděly, kde mají renderovat plynulé přechody.

---

# TileLoader.js & LowresTileLoader.js

## Přehled

Zajišťují fyzické stažení dat ze serveru a jejich převod na Three.js objekty (`Mesh`).

## Vnitřní Logika

- **`pathFromCoords(x, z)`**: Převádí souřadnice na stejnou hierarchickou cestu (`x/1/2/z/3/4`), kterou používá javové
  jádro. Tím se vyhne problémům s limity souborů v adresářích.
- **`PRBMLoader`**: Vlastní binární parser pro formát `.prbm`. Převádí bajty přímo na `BufferGeometry`.
- **`RevalidatingFileLoader`**: Speciální loader, který inteligentně používá cache prohlížeče, ale dokáže vynutit
  kontrolu nové verze, pokud uživatel mapu resetuje.
- **Asynchronní Mesh:** Po načtení geometrie vytvoří `Mesh`, přiřadí mu materiál a nastaví správnou pozici ve světě na
  základě souřadnic dlaždice.
