# StorageType.java

## Přehled

`StorageType` je registr podporovaných typů úložišť. Definuje vztah mezi klíčem v konfiguraci (např. `sql`) a třídou,
která toto nastavení zpracovává.

## Umístění

`de.bluecolored.bluemap.common.config.storage.StorageType`

## Registrované Typy

- **`FILE`**:
    - Klíč: `bluemap:file`
    - Třída: `FileConfig`
- **`SQL`**:
    - Klíč: `bluemap:sql`
    - Třída: `SQLConfig`

## Metody

- `getConfigType()`: Vrátí třídu konfigurace (např. `SQLConfig.class`) pro daný typ.
