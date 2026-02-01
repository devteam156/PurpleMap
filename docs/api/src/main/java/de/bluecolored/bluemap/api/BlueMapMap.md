# BlueMapMap.java

## Přehled

Rozhraní `BlueMapMap` reprezentuje jednu konkrétní mapu (render) určitého světa. Odpovídá jedné položce v seznamu `maps`
v konfiguračním souboru BlueMap.

## Umístění

`de.bluecolored.bluemap.api.BlueMapMap`

## Metody

### `getId()`

Vrací ID mapy (z konfigurace).

### `getName()`

Vrací zobrazované jméno mapy (z konfigurace).

### `getWorld()`

Vrací instanci `BlueMapWorld`, ke které tato mapa patří.

### `getAssetStorage()`

Vrací `AssetStorage` pro tuto mapu. Zde se ukládají soubory (obrázky, data), které jsou specifické pro tuto mapu a mají
být dostupné ve webové aplikaci.

### `getMarkerSets()`

Vrací `Map<String, MarkerSet>`, která obsahuje sady markerů pro tuto mapu.

- Klíčem je ID sady markerů.
- Tato mapa je modifikovatelná. Změny v ní se projeví ve webové aplikaci.

### `getTileSize()`

Vrací velikost dlaždice (tile) v blocích jako `Vector2i`.

### `getTileOffset()`

Vrací posun (offset) mřížky dlaždic v blocích jako `Vector2i`.

### `setFrozen(boolean frozen)`

Zmrazí nebo rozmrazí aktualizace mapy. Pokud je mapa zmrazená, BlueMap ji nebude aktualizovat (vykreslovat změny).

### `isFrozen()`

Vrací `true`, pokud je mapa zmrazená.

### `posToTile(double blockX, double blockZ)`

Převede souřadnice bloku na souřadnice dlaždice mapy (tile coordinate).

### `posToTile(Vector3i pos)`

Převede pozici bloku (`Vector3i`) na souřadnice dlaždice.

### `posToTile(Vector3d pos)`

Převede pozici (`Vector3d`) na souřadnice dlaždice.

### `setTileFilter(Predicate<Vector2i> filter)`

**Zastaralé (Deprecated)**
Nastaví filtr pro dlaždice. Doporučuje se používat konfigurační `render-mask`.

### `getTileFilter()`

**Zastaralé (Deprecated)**
Vrací aktuální filtr dlaždic.
