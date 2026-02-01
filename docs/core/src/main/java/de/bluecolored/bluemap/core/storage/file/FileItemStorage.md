# FileItemStorage.java

## Přehled

`FileItemStorage` je implementace `ItemStorage`, která ukládá jednu položku (soubor) na disk.

## Umístění

`de.bluecolored.bluemap.core.storage.file.FileItemStorage`

## Implementovaná Rozhraní

`ItemStorage`

## Atributy

- `file`: Cesta k souboru.
- `compression`: Komprese dat.
- `atomic`: Zda se má používat atomický zápis (zápis do dočasného souboru a následné přejmenování).

## Metody

### `write()`

Otevře výstupní proud pro zápis do souboru. Pokud je `atomic` zapnuto, používá `FileHelper.createFilepartOutputStream`.
Data jsou komprimována dle nastavení.

### `read()`

Otevře vstupní proud pro čtení ze souboru.

### `delete()`

Smaže soubor.

### `exists()`

Zkontroluje, zda soubor existuje.
