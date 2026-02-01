# ResourcePool.java

## Přehled

`ResourcePool` je obecná třída pro správu a cachování zdrojů (resources) načtených z balíčků. Umožňuje mapovat `Key` (
identifikátor) na konkrétní objekt zdroje.

## Umístění

`de.bluecolored.bluemap.core.resources.pack.ResourcePool`

## Generika

- `<T>`: Typ zdroje (např. `BlockStateResource`, `Texture`).

## Funkcionalita

- Udržuje mapu `Key -> T` (načtené zdroje).
- Udržuje mapu `Key -> ResourcePath<T>` (cesty ke zdrojům).
- Je thread-safe (používá synchronizované metody).

## Metody

### `put(Key path, T value)`

Vloží zdroj do poolu.

### `get(Key path)`

Získá zdroj z poolu. Pokud je zdroj definován pouze cestou (`ResourcePath`) a ještě nebyl načten, pokusí se ho načíst (
lazy loading).

### `load(ResourcePath<T> path, Loader<T> loader)`

Načte zdroj pomocí loaderu a vloží ho do poolu. Pokud zdroj již existuje, ignoruje ho (první vyhrává).

### `load(ResourcePath<T> path, Loader<T> loader, BinaryOperator<T> mergeFunction)`

Načte zdroj a pokud již existuje, sloučí nový zdroj s existujícím pomocí `mergeFunction`.
