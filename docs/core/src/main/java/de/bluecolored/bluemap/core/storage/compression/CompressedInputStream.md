# CompressedInputStream.java

## Přehled

`CompressedInputStream` je dekorátor pro `InputStream`, který si pamatuje typ komprese dat, která čte.

## Umístění

`de.bluecolored.bluemap.core.storage.compression.CompressedInputStream`

## Dědičnost

`DelegateInputStream` -> `CompressedInputStream`

## Metody

### `decompress()`

Vrátí nový `InputStream` (dekomprimovaný), který vznikne aplikací příslušného dekompresoru na původní stream.

### `getCompression()`

Vrátí typ komprese (`Compression`).
