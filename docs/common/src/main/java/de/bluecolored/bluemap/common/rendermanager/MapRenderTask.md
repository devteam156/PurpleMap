# MapRenderTask.java

## Přehled

`MapRenderTask` je rozšiřující rozhraní pro `RenderTask`, které přidává vazbu na konkrétní mapu.

## Umístění

`de.bluecolored.bluemap.common.rendermanager.MapRenderTask`

## Metody

### `getMap()`

Vrátí instanci `BmMap`, ke které úloha patří. To umožňuje manažerovi nebo příkazům filtrovat a seskupovat úlohy podle
mapy.
