# MapUpdateService.java

## Přehled

`MapUpdateService` je služba (běžící ve vlastním vlákně), která sleduje změny v souborech regionů světa a automaticky
plánuje aktualizace odpovídajících částí mapy.

## Umístění

`de.bluecolored.bluemap.common.plugin.MapUpdateService`

## Dědičnost

`Thread` -> `MapUpdateService`

## Funkcionalita

- Používá `WatchService` z jádra BlueMap k detekci změn souborů `.mca`.
- Implementuje mechanismus odložení (debounce/delay): po detekci změny čeká určitý čas (konfigurovatelný
  `updateCooldown`, minimálně 5s), než naplánuje renderování. To zabraňuje zbytečnému pře-renderování, pokud se soubor
  mění často (např. při aktivním hraní).
- Využívá `Timer` pro plánování opožděných úloh.

## Metody

### `run()`

Hlavní smyčka vlákna. Čeká na události z `WatchService` a volá `updateRegion`.

### `updateRegion(Vector2i regionPos)`

Zpracuje událost změny regionu.

- Zruší případnou předchozí naplánovanou úlohu pro tento region.
- Naplánuje novou úlohu, která po uplynutí cooldownu vytvoří `WorldRegionRenderTask` a přidá ho do `RenderManageru`.

### `close()`

Zastaví službu, přeruší vlákno a uzavře zdroje.
