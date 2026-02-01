# BufferedCompression.java

## Přehled

`BufferedCompression` je obecná implementace `Compression`, která obaluje libovolný `StreamTransformer` (funkci
transformující stream). Automaticky obaluje streamy do `BufferedInputStream` / `BufferedOutputStream` pro lepší výkon.

## Umístění

`de.bluecolored.bluemap.core.storage.compression.BufferedCompression`

## Konstruktory

- `key`: Identifikátor komprese (Key).
- `id`: Textové ID.
- `fileSuffix`: Přípona souboru (např. `.gz`).
- `compressor`: Funkce pro vytvoření kompresního OutputStreamu.
- `decompressor`: Funkce pro vytvoření dekompresního InputStreamu.

## Metody

Implementuje metody rozhraní `Compression`.
