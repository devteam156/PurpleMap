# MapRequestHandler.java

## Přehled

`MapRequestHandler` je specializovaný router pro jednu konkrétní mapu. Skládá dohromady `MapStorageRequestHandler` (pro
statická data) a `JsonDataRequestHandler`y (pro živá data).

## Umístění

`de.bluecolored.bluemap.common.web.MapRequestHandler`

## Dědičnost

`RoutingRequestHandler` -> `MapRequestHandler`

## Funkcionalita

- V konstruktoru zaregistruje trasy:
    - `.*` -> `MapStorageRequestHandler` (vše ostatní jde do úložiště).
    - `live/players.json` -> `JsonDataRequestHandler` s `LivePlayersDataSupplier` (pokud je dostupný).
    - `live/markers.json` -> `JsonDataRequestHandler` s `LiveMarkersDataSupplier` (pokud je dostupný).
- Používá `CachedRateLimitDataSupplier` pro živá data, aby nedocházelo k přetížení serveru příliš častým generováním
  JSONů.