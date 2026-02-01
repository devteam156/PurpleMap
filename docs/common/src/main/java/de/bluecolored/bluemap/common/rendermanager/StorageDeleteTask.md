# StorageDeleteTask.java

## Přehled

`StorageDeleteTask` je úloha zaměřená čistě na smazání dat v úložišti (storage) bez ovlivnění vnitřního stavu `BmMap` v
paměti (na rozdíl od `MapPurgeTask`).

## Umístění

`de.bluecolored.bluemap.common.rendermanager.StorageDeleteTask`

## Implementovaná Rozhraní

- `RenderTask`

## Atributy

- `storage`: Instance `MapStorage`, ze které se mažou data.
- `mapId`: Identifikátor mapy, jejíž data mají být smazána.

## Vnitřní Logika a Metody

### `doWork()`

Zavolá metodu `storage.delete(callback)`. Tato metoda prochází fyzické soubory (nebo řádky v DB) a odstraňuje je. Průběh
je reportován přes callback do atributu `progress`.

### `contains(RenderTask task)`

Vrací `true`, pokud je cílové úložiště a ID mapy shodné.
