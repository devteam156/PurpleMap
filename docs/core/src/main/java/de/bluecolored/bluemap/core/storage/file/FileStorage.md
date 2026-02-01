# FileStorage.java

## Přehled

`FileStorage` je hlavní vstupní bod pro souborové úložiště. Spravuje více map (`FileMapStorage`).

## Umístění

`de.bluecolored.bluemap.core.storage.file.FileStorage`

## Implementovaná Rozhraní

`Storage`

## Metody

### `map(String mapId)`

Vrátí `FileMapStorage` pro dané ID mapy.

### `mapIds()`

Vrátí stream ID všech map, které v úložišti existují (adresáře v kořenové složce).
