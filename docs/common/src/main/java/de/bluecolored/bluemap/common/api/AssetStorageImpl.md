# AssetStorageImpl.java

## Přehled

`AssetStorageImpl` je implementace rozhraní `AssetStorage`. Zprostředkovává přístup k úložišti assetů (obrázků, dat) pro
konkrétní mapu.

## Umístění

`de.bluecolored.bluemap.common.api.AssetStorageImpl`

## Implementovaná Rozhraní

`AssetStorage`

## Konstruktory

### `AssetStorageImpl(MapStorage storage, String mapId)`

Vytvoří novou instanci úložiště assetů.

- `storage`: Interní `MapStorage` (z jádra BlueMap), které fyzicky spravuje data.
- `mapId`: ID mapy, ke které toto úložiště patří.

## Metody

### `writeAsset(String name)`

Vytvoří a vrátí `OutputStream` pro zápis nového assetu do `MapStorage`.

### `readAsset(String name)`

Vrátí `Optional<InputStream>` pro čtení assetu. Pokud jsou data v úložišti komprimována, automaticky je dekomprimuje.

### `assetExists(String name)`

Zkontroluje existenci assetu v `MapStorage`.

### `getAssetUrl(String name)`

Vrátí relativní URL pro přístup k assetu.

- Formát: `maps/{mapId}/assets/{name}`
- Jméno assetu je escapováno, aby bylo bezpečné pro URL.

### `deleteAsset(String name)`

Smaže asset z `MapStorage`.
