# LowresTileManager.java

## Přehled

`LowresTileManager` spravuje hierarchii low-res vrstev (LOD - Level of Detail). Slouží jako vstupní bod pro zápis dat do
přehledové mapy z renderovacího procesu (`HiresModelManager`).

## Umístění

`de.bluecolored.bluemap.core.map.lowres.LowresTileManager`

## Implementovaná Rozhraní

`TileMetaConsumer`

## Atributy

- `tileGrid`: Mřížka definující rozložení dlaždic.
- `lodFactor`: Faktor zmenšení mezi vrstvami (např. 5).
- `lodCount`: Počet vrstev detailů.
- `layers`: Pole `LowresLayer` objektů seřazené od nejdetailnější (LOD 0) po nejméně detailní.

## Metody

### `set(int x, int z, Color color, int height, int blockLight)`

Zapisuje data pixelu (barvu, výšku, světlo) na globálních souřadnicích `x, z`.

- Tato data se zapíší do nejnižší vrstvy (`layers[0]`).
- Tato vrstva se pak postará o propagaci změn do vyšších vrstev (průměrování).

### `save()`

Uloží všechny změny ve všech vrstvách na disk.

### `discard()`

Zahodí všechny neuložené změny.
