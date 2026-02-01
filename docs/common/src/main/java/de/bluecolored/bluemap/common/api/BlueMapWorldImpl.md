# BlueMapWorldImpl.java

## Přehled

`BlueMapWorldImpl` je implementace rozhraní `BlueMapWorld`. Obaluje interní objekt `World` z jádra BlueMap.

## Umístění

`de.bluecolored.bluemap.common.api.BlueMapWorldImpl`

## Implementovaná Rozhraní

`BlueMapWorld`

## Konstruktory

### `BlueMapWorldImpl(World world, BlueMapService blueMapService, Plugin plugin)`

Vytvoří novou instanci obalující `World`.

## Metody

### `getId()`

Vrací ID světa (např. identifikátor dimenze nebo UUID).

### `getSaveFolder()`

**Zastaralé (Deprecated)**
Vrací cestu k složce světa. Funguje pouze pokud je svět typu `MCAWorld` (svět založený na Anvil/MCA formátu). Jinak
vyhodí `UnsupportedOperationException`.

### `getMaps()`

Vrací kolekci všech map (`BlueMapMapImpl`), které jsou přiřazeny k tomuto světu. Mapy jsou filtrovány z globálního
seznamu map v `BlueMapService`.

### `world()`

Pomocná metoda pro získání interního objektu `World`.
