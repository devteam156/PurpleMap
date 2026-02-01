# AssetStorage.java

## Přehled

Rozhraní `AssetStorage` poskytuje abstrakci pro ukládání a čtení "assetů" (souborů) specifických pro danou mapu. Assety
mohou být obrázky (ikony pro markery), skripty, JSON soubory nebo jakákoli jiná data, která potřebujete zpřístupnit pro
webovou aplikaci BlueMap.

## Umístění

`de.bluecolored.bluemap.api.AssetStorage`

## Metody

### `writeAsset(String name)`

Otevře `OutputStream` pro zápis nového assetu.

- Pokud asset s daným jménem již existuje, bude přepsán.
- Data se fyzicky uloží až po uzavření streamu.
- **Parametry:** `name` - unikátní název assetu (např. "my-icon.png").
- **Vrací:** `OutputStream` pro zápis dat.

### `readAsset(String name)`

Pokusí se načíst existující asset.

- **Parametry:** `name` - název assetu.
- **Vrací:** `Optional<InputStream>` s daty assetu, nebo prázdný Optional, pokud asset neexistuje.

### `assetExists(String name)`

Rychle zkontroluje, zda asset s daným názvem v úložišti existuje, bez nutnosti otevírat stream.

- **Vrací:** `true` pokud existuje, jinak `false`.

### `getAssetUrl(String name)`

Vrátí relativní URL adresu, kterou může webová aplikace (prohlížeč) použít k načtení tohoto assetu.

- Tuto URL lze použít například v metodách `setIcon` u markerů.
- Metoda vrací validní URL i v případě, že asset zatím neexistuje (předpokládá se, že bude vytvořen).

### `deleteAsset(String name)`

Smaže asset z úložiště. Pokud asset neexistuje, nestane se nic.
