# MapSettings.java

## Přehled

`MapSettings` je rozhraní definující konfiguraci mapy. Rozšiřuje `RenderSettings` o vlastnosti specifické pro mapu jako
celek (nejen pro renderování modelu).

## Umístění

`de.bluecolored.bluemap.core.map.MapSettings`

## Dědičnost

`RenderSettings` -> `MapSettings`

## Metody (Vlastnosti)

### `getSorting()`

Pořadí mapy v seznamu.

### `getStartPos()`

Výchozí pozice kamery.

### `getSkyColor()`, `getVoidColor()`

Barvy pozadí.

### `getMinInhabitedTime()`, `getMinInhabitedTimeRadius()`

Filtrování chunků podle času stráveného hráči (pro generování pouze obydlených oblastí).

### `getHiresTileSize()`, `getLowresTileSize()`

Velikost dlaždic (v blocích).

### `getLodCount()`, `getLodFactor()`

Nastavení úrovní detailů (Level of Detail) pro low-res mapu.

### `getSkyLight()`

Úroveň nebeského světla (ovlivňuje jas).

### `isEnablePerspectiveView()`, `isEnableFlatView()`, `isEnableFreeFlightView()`

Povolení/zakázání různých režimů kamery ve webové aplikaci.

### `isEnableHires()`

Zda se má generovat a zobrazovat high-res (detailní) mapa.

### `isCheckForRemovedRegions()`

Zda se má kontrolovat, jestli byly regiony smazány ze světa (a následně je smazat z mapy).
