# BlueMapMapImpl.java

## Přehled

`BlueMapMapImpl` je implementace rozhraní `BlueMapMap`. Slouží jako obálka (wrapper) kolem interního objektu `BmMap` z
jádra BlueMap, vystavující jeho funkcionalitu přes veřejné API.

## Umístění

`de.bluecolored.bluemap.common.api.BlueMapMapImpl`

## Implementovaná Rozhraní

`BlueMapMap`

## Konstruktory

### `BlueMapMapImpl(BmMap map, BlueMapWorldImpl world, Plugin plugin)`

Vytvoří novou instanci obalující `BmMap`. Používá `WeakReference` pro interní objekty, aby se zabránilo memory leakům
při reloadu pluginu.

## Metody

### `getId()`

Vrací ID mapy.

### `getName()`

Vrací jméno mapy.

### `getWorld()`

Vrací instanci `BlueMapWorldImpl` příslušející této mapě.

### `getAssetStorage()`

Vytváří a vrací novou instanci `AssetStorageImpl` pro tuto mapu.

### `getMarkerSets()`

Vrací mapu sad markerů (`MarkerSet`) přímo z interního objektu mapy.

### `getTileSize()` a `getTileOffset()`

Vrací informace o mřížce dlaždic (velikost a posun) z modelu s vysokým rozlišením.

### `setFrozen(boolean frozen)`

Zmrazí nebo rozmrazí mapu.

- **Zmrazení:** Zastaví sledování změn v mapě a zruší všechny naplánované úlohy renderování pro tuto mapu.
- **Rozmrazení:** Znovu aktivuje sledování a naplánuje kontrolu aktualizací.

### `isFrozen()`

Vrací `true`, pokud je mapa zmrazená (aktualizace jsou vypnuté).

### `map()`

Pomocná metoda pro získání interního objektu `BmMap`.
