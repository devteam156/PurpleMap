# TileMetaConsumer.java

## Přehled

`TileMetaConsumer` je funkcionální rozhraní, které slouží jako callback pro předávání metadat o vyrenderované dlaždici.

## Umístění

`de.bluecolored.bluemap.core.map.TileMetaConsumer`

## Použití

Používá se primárně k přenosu informací z `HiresModelManager` (který renderuje detailní model) do `LowresTileManager` (
který potřebuje průměrnou barvu, výšku a světlo pro vytvoření pixelu na přehledové mapě).

## Metody

### `set(int x, int z, Color color, int height, int blockLight)`

Zaznamená metadata pro jeden sloupec bloků na dané souřadnici (relativní k dlaždici?).

- `x`, `z`: Souřadnice.
- `color`: Průměrná barva shora viditelného bloku.
- `height`: Výška terénu.
- `blockLight`: Úroveň světla z bloků.
