# BmMap.java (Srdce Mapy)

## Přehled

`BmMap` je hlavní třída reprezentující jednu vyrenderovanou mapu. Drží v sobě všechny komponenty potřebné pro proces
transformace Minecraft světa do webového vieweru.

## Umístění

`de.bluecolored.bluemap.core.map.BmMap`

## Atributy a Komponenty

### Základní Data

- `id`: Unikátní řetězec (např. "overworld").
- `name`: Lidsky čitelný název (např. "Overworld").
- `world`: Instance `World`, ze které se čtou data.
- `storage`: Instance `MapStorage`, kam se ukládají výsledky.
- `mapSettings`: Konfigurace specifická pro tuto mapu.

### Renderovací Manažeři

- **`hiresModelManager`**: Spravuje generování detailních 3D modelů (`.prbm`).
- **`lowresTileManager`**: Spravuje generování 2D dlaždic (`.png`) pro různé úrovně přiblížení (LOD).

### Správa Stavu

- **`mapTileState`**: Pamatuje si, kdy byla která dlaždice naposledy vyrenderována.
- **`mapChunkState`**: Pamatuje si hashy chunků, aby se vědělo, co se změnilo.
- **`textureGallery`**: Registr všech textur použitých v mapě.

## Vnitřní Logika a Metody

### Konstruktor

1. Inicializuje úložiště stavů (`MapTileState`, `MapChunkState`).
2. Načte `textureGallery` z úložiště nebo vytvoří novou z ResourcePacku.
3. Vytvoří `HiresModelManager` s mřížkou posunutou o 2 bloky (zajišťuje překryv pro správné renderování sousedních
   bloků).
4. Vytvoří `LowresTileManager`.
5. Uloží aktuální nastavení mapy do `settings.json`.

### `renderTile(Vector2i tile)`

- **Logika:** Hlavní entrypoint pro renderování jedné dlaždice.
    1. Zkontroluje `tileFilter` (např. zda dlaždice spadá do render-boundaries).
    2. Spustí stopky (měření průměrného času na dlaždici).
    3. Zavolá `hiresModelManager.render(...)`. Tento proces zároveň aktualizuje příslušné pixely v nízkorozlišených
       vrstvách přes `lowresTileManager`.
    4. Uloží statistiky o čase.

### `save()` (Synchronizováno)

- **Logika:** Kompletní perzistence stavu mapy.
    - Uloží `lowres` dlaždice (obrázky).
    - Uloží stavy dlaždic a chunků (binary dat).
    - Uloží markery a pozice hráčů.
    - Uloží `textureGallery` (pouze pokud na disku chybí, aby se zamezilo zbytečnému zápisu velkého JSONu).

---

# TextureGallery.java

## Přehled

`TextureGallery` funguje jako "telefonní seznam" pro textury. Přiřazuje každé unikátní textuře (ResourcePath) číselné
ID (index).

## Proč je to důležité?

V 3D modelech BlueMap (`.prbm`) se nepoužívají názvy textur (např. `minecraft:block/stone`), ale pouze jejich číselné
indexy. To drasticky zmenšuje velikost modelů. Webový prohlížeč pak pomocí `textures.json` (který generuje tato třída)
ví, který index patří ke kterému obrázku.

## Vnitřní Logika

- **Řazení:** Metoda `put(ResourcePool)` řadí textury tak, aby **průhledné textury byly na konci**. To je důležité pro
  webový prohlížeč kvůli správnému pořadí vykreslování (Transparency Sorting).
- **`writeTexturesFile`**: Generuje pole objektů Texture do JSONu. Pokud textura v poolu chybí, použije se
  `MISSING_TEXTURE`.

---

# MapSettings.java (Rozhraní)

## Přehled

Definuje všechny parametry, které ovlivňují chování mapy a rendereru.

## Klíčové parametry

- `getHiresTileSize()` / `getLowresTileSize()`: Rozměry mřížek.
- `getLodCount()`: Počet úrovní zmenšení mapy.
- `isEnablePerspectiveView()` / `isEnableFlatView()`: Dostupné režimy ve vieweru.
- `isRenderTopOnly()`: Optimalizace – pokud je aktivní jen 2D pohled, BlueMap nerenderuje stěny bloků, které nejsou
  vidět shora.
