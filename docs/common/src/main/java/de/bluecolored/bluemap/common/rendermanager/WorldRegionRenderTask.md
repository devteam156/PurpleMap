# WorldRegionRenderTask.java

## Přehled

`WorldRegionRenderTask` je základní jednotkou práce v renderovacím procesu BlueMap. Tato třída zodpovídá za kompletní
aktualizaci jednoho regionu (typicky 32x32 chunků, tj. 512x512 bloků). Je navržena tak, aby její metodu `doWork()` mohlo
volat více vláken současně, čímž dochází k paralelnímu renderování dlaždic (tiles) v rámci jednoho regionu.

## Umístění

`de.bluecolored.bluemap.common.rendermanager.WorldRegionRenderTask`

## Balíček

`de.bluecolored.bluemap.common.rendermanager`

## Implementovaná Rozhraní

- `MapRenderTask` (které dědí od `RenderTask`)

## Atributy a Stavové Proměnné

### Konfigurační Atributy

- `map`: Instance `BmMap`, pro kterou se renderuje.
- `regionPos`: Souřadnice regionu (`Vector2i`).
- `force`: `TileUpdateStrategy` určující, zda se má vynutit přegenerování i nezměněných dlaždic.

### Mřížky (Grids)

- `regionGrid`: Mřížka regionů světa.
- `chunkGrid`: Mřížka chunků světa.
- `tileGrid`: Mřížka dlaždic mapy (hires modelů).

### Rozsahy (Bounds)

- `chunkMin`, `chunkMax`: Rozsah chunků v tomto regionu.
- `chunksSize`: Počet chunků v ose X a Z (obvykle 32x32).
- `tileMin`, `tileMax`: Rozsah dlaždic (tiles), které tento region pokrývá.
- `tileSize`: Počet dlaždic v ose X a Z.

### Datová Pole

- `chunkHashes`: Pole `int[]` obsahující časová razítka (last modified) všech chunků v regionu v momentě spuštění úlohy.
- `tileActions`: Pole `ActionAndNextState[]`, které pro každou dlaždici uchovává rozhodnutí, co se s ní má udělat (
  RENDER, DELETE, NONE).

### Řízení Průběhu (Volatile)

- `nextTileX`, `nextTileZ`: Indexy příští dlaždice ke zpracování. Používají se pro koordinaci mezi vlákny.
- `atWork`: Počet vláken, která právě aktivně pracují na tomto tasku.
- `completed`: Příznak, že byly naplánovány všechny dlaždice.
- `cancelled`: Příznak ručního zrušení úlohy.

## Konstruktory

Třída poskytuje tři varianty konstruktoru, které se liší způsobem nastavení strategie `force`. Všechny nakonec
inicializují základní stav (indexy na 0, completed/cancelled na false).

## Vnitřní Logika a Metody

### `init()` (Synchronizováno)

Tato metoda se volá jednou, při prvním zavolání `doWork()`. Provádí náročnou přípravu:

1. **Výpočet hranic:** Převede souřadnice regionu na rozsahy chunků a dlaždic pomocí mřížek.
2. **Načtení hashů chunků:**
    - Otevře region soubor světa.
    - Projde všechny chunky a uloží jejich timestampy do `chunkHashes`.
    - Volá `invalidateChunkCache(x, z)`, aby zajistila, že se při renderování budou číst čerstvá data.
3. **Rozhodovací proces (Tile Actions):**
    - Pro každou dlaždici v regionu vypočítá index v poli `tileActions`.
    - Zjistí aktuální stav dlaždice z `map.getMapTileState()`.
    - Zavolá `tileState.findActionAndNextState(...)`. Rozhodnutí závisí na:
        - `force`: Zda je vynucen update.
        - `checkChunksHaveChanges(tile)`: Zda se změnil alespoň jeden chunk pod dlaždicí.
        - `checkTileBounds(tile)`: Zda je dlaždice uvnitř hranic renderování (RENDER), na okraji (EDGE -> DELETE/NONE)
          nebo úplně mimo (DELETE).
4. **Optimalizace:** Pokud je třeba renderovat více než 75 % dlaždic, zavolá `map.getWorld().preloadRegionChunks(...)`
   pro masivní zrychlení následného čtení.

### `doWork()`

Hlavní pracovní metoda volaná worker thready z `RenderManager`u.

1. **Atomické získání práce:** V `synchronized` bloku získá aktuální `tileX` a `tileZ` a inkrementuje indexy pro další
   vlákno. Pokud je dosaženo konce, nastaví `completed = true`. Inkrementuje `atWork`.
2. **Zpracování:** Zavolá `processTile(tileX, tileZ)`. Tato část běží **mimo** synchronizovaný blok, tedy paralelně.
3. **Ukončení:** V `synchronized` bloku dekrementuje `atWork`. Pokud je `atWork == 0` a vše je hotovo, zavolá
   `complete()`.

### `processTile(int x, int z)`

Provádí samotnou modifikaci mapy:

1. Získá souřadnice dlaždice a plánovanou akci.
2. **NONE:** Pouze nastaví stav dlaždice na cílový.
3. **RENDER:**
    - Nejdříve zkontroluje `checkTileRenderPreconditions` (zda jsou chunky generované, zda mají světlo atd.).
    - Pokud selžou, zavolá `unrenderTile` (smaže starý model) a nastaví chybový stav.
    - Pokud projdou, zavolá `map.renderTile(tile)`.
4. **DELETE:** Zavolá `map.unrenderTile(tile)`.
5. **Finále:** V bloku `finally` zapíše nový stav do `MapTileState` (včetně aktuálního času).

### `complete()` (Synchronizováno)

Finalizace po zpracování všech dlaždic regionu:

1. **Uložení změn chunků:** Zapíše hodnoty z `chunkHashes` do `MapChunkState`. Díky tomu BlueMap příště pozná, že se
   chunky nezměnily a nemusí dlaždici znovu renderovat.
2. **Uvolnění paměti:** Nastaví `chunkHashes` a `tileActions` na `null`.
3. **Uložení na disk:** Zavolá `map.save()`.

### Pomocné metody pro rozhodování

- `checkChunksHaveChanges(Vector2i tile)`: Porovnává aktuální timestampy chunků s těmi uloženými v `MapChunkState`.
  Stačí jedna změna a dlaždice se musí přerenderovat.
- `checkTileBounds(Vector2i tile)`: Kontroluje, zda dlaždice spadá do `render-boundaries` nastavených v konfiguraci
  mapy.
- `checkTileRenderPreconditions(Vector2i tile)`:
    - Ověřuje `min-inhabited-time` (podmínka pro potlačení renderování prázdných oblastí).
    - Ověřuje přítomnost světelných dat (pokud není zapnuto `ignore-missing-light-data`).
    - Pokud narazí na poškozený chunk, vrátí `CHUNK_ERROR`.
