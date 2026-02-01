# StorageConfig.java

## Přehled

`StorageConfig` je abstraktní základ pro všechny konfigurační třídy úložišť. Obsahuje společnou logiku pro parsování
typů a definuje kontrakt pro vytvoření instance úložiště.

## Umístění

`de.bluecolored.bluemap.common.config.storage.StorageConfig`

## Balíček

`de.bluecolored.bluemap.common.config.storage`

## Atributy

- `storageType`: `String` - Identifikátor typu úložiště (např. "file" nebo "sql").

## Metody

### `getStorageType()`

- **Logika:** Převede textový řetězec `storageType` na objekt `StorageType` pomocí registru. Podporuje i starší formáty
  klíčů (legacy).

### `createStorage()`

- **Popis:** Abstraktní tovární metoda. Každá konkrétní konfigurace musí implementovat tuto metodu a vrátit plně
  zinicializovanou instanci `Storage` (např. `SQLStorage`).

### `parseKey(...)` (Statická pomocná)

- **Logika:** Univerzální parser pro klíče v registrech. Zkouší najít klíč v daném registru, přičemž řeší
  case-insensitivitu a výchozí jmenné prostory (`bluemap:`).