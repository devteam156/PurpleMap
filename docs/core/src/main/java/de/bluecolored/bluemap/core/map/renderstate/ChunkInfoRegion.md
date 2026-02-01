# ChunkInfoRegion.java

## Přehled

`ChunkInfoRegion` reprezentuje data o stavu chunků v jednom regionu (oblast 32x32 chunků). Konkrétně ukládá **hashe**
chunků (timestampy poslední změny). Používá se k detekci, které chunky se změnily a je třeba je přegenerovat.

## Umístění

`de.bluecolored.bluemap.core.map.renderstate.ChunkInfoRegion`

## Implementovaná Rozhraní

`CellStorage.Cell`

## Atributy

- `chunkHashes`: Pole intů o velikosti 1024 (32*32). Každý int je hash chunku.
- `modified`: Příznak, zda došlo ke změně dat.

## Metody

### `get(int x, int z)`

Vrátí hash chunku na lokálních souřadnicích regionu (0-31).

### `set(int x, int z, int hash)`

Nastaví hash chunku. Pokud se hash liší od původního, nastaví `modified = true`.

### `init()`

Inicializuje pole hashů (voláno po deserializaci).
