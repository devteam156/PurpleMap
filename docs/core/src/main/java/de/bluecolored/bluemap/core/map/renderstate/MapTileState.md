# MapTileState.java

## Přehled

`MapTileState` je specializované `CellStorage`, které uchovává informace o stavu renderování dlaždic (tiles). Pro každou
dlaždici si pamatuje, kdy byla naposledy vyrenderována a v jakém je stavu (např. `RENDERED`, `MISSING_LIGHT`).

## Umístění

`de.bluecolored.bluemap.core.map.renderstate.MapTileState`

## Dědičnost

`CellStorage<TileInfoRegion>` -> `MapTileState`

## Funkcionalita

- Dělí mapu na regiony o velikosti 32x32 dlaždic.
- Každá buňka (`TileInfoRegion`) uchovává informace o 1024 dlaždicích.
- Sleduje `lastRenderTime` (globální maximum), což pomáhá při inkrementálních aktualizacích.

## Metody

### `get(int x, int z)`

Vrátí `TileInfo` (čas renderu a stav) pro dlaždici na souřadnicích `x, z`.

### `set(int x, int z, TileInfoRegion.TileInfo info)`

Aktualizuje informace o dlaždici.
