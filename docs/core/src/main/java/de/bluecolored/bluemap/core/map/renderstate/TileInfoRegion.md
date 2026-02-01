# TileInfoRegion.java

## Přehled

`TileInfoRegion` je datová struktura (buňka) používaná v `MapTileState`. Uchovává stav a čas posledního renderu pro
oblast 32x32 dlaždic.

## Umístění

`de.bluecolored.bluemap.core.map.renderstate.TileInfoRegion`

## Implementovaná Rozhraní

`CellStorage.Cell`

## Atributy

- `lastRenderTimes`: Pole intů (timestampy renderování).
- `tileStates`: Pole `TileState` (stav dlaždice, např. RENDERED). Používá paletizaci při serializaci (NBT) pro úsporu
  místa.

## Metody

### `get(int x, int z)`

Vrátí `TileInfo` pro lokální souřadnice v regionu.

### `set(int x, int z, TileInfo info)`

Nastaví informace pro dlaždici.

### `init()`

Inicializuje pole po deserializaci.

## Vnořená třída `TileInfo`

Jednoduchý přepravka (data class) pro `renderTime` a `TileState`.
