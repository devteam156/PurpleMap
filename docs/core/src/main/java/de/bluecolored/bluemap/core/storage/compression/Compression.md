# Compression.java

## Přehled

`Compression` je rozhraní (a registr) definující různé typy komprese dat.

## Umístění

`de.bluecolored.bluemap.core.storage.compression.Compression`

## Implementovaná Rozhraní

`Keyed`

## Konstanty / Registry

- `NONE`: Žádná komprese.
- `GZIP`: GZIP komprese (standard).
- `DEFLATE`: Deflate komprese.
- `ZSTD`: Zstandard komprese (rychlá a efektivní).
- `LZ4`: LZ4 komprese (velmi rychlá dekomprese).

## Metody

### `compress(OutputStream out)`

Vrátí stream, který komprimuje zapisovaná data.

### `decompress(InputStream in)`

Vrátí stream, který dekomprimuje čtená data.

### `getFileSuffix()`

Vrátí příponu souboru používanou pro tento typ komprese.
