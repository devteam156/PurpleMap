# MapChunkState.java

## Přehled

`MapChunkState` je specializované `CellStorage`, které uchovává informace o stavu chunků (konkrétně jejich hashe).
Používá se k detekci změn v chuncích, aby se předešlo zbytečnému renderování nezměněných oblastí.

## Umístění

`de.bluecolored.bluemap.core.map.renderstate.MapChunkState`

## Dědičnost

`CellStorage<ChunkInfoRegion>` -> `MapChunkState`

## Funkcionalita

- Dělí svět na regiony (buňky) o velikosti 32x32 chunků (což odpovídá velikosti MCA region souborů).
- Každá buňka (`ChunkInfoRegion`) uchovává hashe pro 1024 chunků.
- Umožňuje rychle získat a nastavit hash chunku na globálních souřadnicích.

## Metody

### `get(int x, int z)`

Vrátí uložený hash chunku na souřadnicích `x, z`.

### `set(int x, int z, int hash)`

Nastaví nový hash chunku. Vrátí předchozí hodnotu.
