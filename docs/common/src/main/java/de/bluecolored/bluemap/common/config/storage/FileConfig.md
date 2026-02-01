# FileConfig.java

## Přehled

`FileConfig` konfiguruje ukládání mapových dlaždic přímo jako soubory na disk.

## Umístění

`de.bluecolored.bluemap.common.config.storage.FileConfig`

## Atributy

- `root`: `Path` - Cesta ke kořenovému adresáři, kde budou data uložena (např. `bluemap/web/maps`).
- `compression`: Typ komprese souborů (GZIP).
- `atomic`: `boolean` - Zda používat atomický zápis souborů (zápis do dočasného souboru a následné přejmenování). Brání
  poškození dat při pádu serveru.

## Metody

### `createStorage()`

- **Logika:** Vrátí instanci `FileStorage` s nakonfigurovanou cestou a kompresí.