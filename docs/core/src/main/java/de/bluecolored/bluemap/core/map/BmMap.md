# BmMap.java

## Přehled

`BmMap` (BlueMap Map) je klíčová třída v jádru BlueMap. Reprezentuje jednu vyrenderovanou mapu. Sdružuje všechny
komponenty potřebné pro její fungování: nastavení, úložiště dat, správce modelů (high-res a low-res), textury a stavy.

## Umístění

`de.bluecolored.bluemap.core.map.BmMap`

## Hlavní komponenty

- **World (`World`)**: Zdrojový svět Minecraftu.
- **Storage (`MapStorage`)**: Úložiště pro výstupní data (dlaždice, nastavení).
- **Settings (`MapSettings`)**: Konfigurace mapy.
- **HiresModelManager**: Správce pro renderování detailního modelu (vysoké rozlišení).
- **LowresTileManager**: Správce pro renderování přehledové mapy (nízké rozlišení).
- **MapTileState / MapChunkState**: Udržují informace o stavu vyrenderovaných dlaždic a hashů chunků (pro inkrementální
  aktualizace).
- **MarkerSets**: Kolekce markerů na mapě.

## Metody

### `renderTile(Vector2i tile)`

Vykreslí jednu dlaždici mapy (high-res) na zadaných souřadnicích.

- Pokud je dlaždice filtrována (`tileFilter`), přeskočí se.
- Měří čas renderování pro statistiky.
- Výsledek renderování předá do `LowresTileManager` pro aktualizaci low-res mapy.

### `unrenderTile(Vector2i tile)`

Smaže vyrenderovanou dlaždici.

### `save()`

Uloží veškerý stav mapy do úložiště:

- Low-res dlaždice.
- Stavy dlaždic a chunků.
- Markery a hráče.
- Nastavení mapy.
- Textury (pokud ještě nejsou uloženy).

### `save(long minTimeSinceLastSave)`

Uloží mapu, pouze pokud od posledního uložení uběhla určitá doba. Používá se pro periodické ukládání během renderování.

### `resetTextureGallery()`

Znovu načte textury z resource packu.

### `getAverageNanosPerTile()`

Vrátí průměrný čas renderování jedné dlaždice v nanosekundách.
