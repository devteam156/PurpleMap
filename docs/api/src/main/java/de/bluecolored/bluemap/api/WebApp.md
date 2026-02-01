# WebApp.java

## Přehled

Rozhraní `WebApp` umožňuje interakci s webovou částí aplikace BlueMap. Poskytuje metody pro registraci vlastních stylů a
skriptů, správu viditelnosti hráčů a přístup k webovému kořenovému adresáři.

## Umístění

`de.bluecolored.bluemap.api.WebApp`

## Metody

### `getWebRoot()`

Vrací cestu (`Path`) ke konfigurovanému kořenovému adresáři webu. Zde se nachází soubory webové aplikace (index.html,
js, css, assets).

### `setPlayerVisibility(UUID player, boolean visible)`

**Experimentální**
Nastaví viditelnost markeru konkrétního hráče na mapě.

- `player`: UUID hráče.
- `visible`: `true` pro zobrazení, `false` pro skrytí.

### `getPlayerVisibility(UUID player)`

**Experimentální**
Vrací aktuální nastavení viditelnosti pro daného hráče.

### `registerStyle(String url)`

Zaregistruje vlastní CSS soubor, který webová aplikace načte.

- Tato metoda by se měla volat pouze uvnitř callbacku `BlueMapAPI.onEnable()`.
- Registrace **není perzistentní**, musí se provést při každém startu/enable BlueMap.
- `url`: Relativní cesta k CSS souboru (vzhledem k web-root). Soubor lze vytvořit pomocí `getWebRoot()`.

### `registerScript(String url)`

Zaregistruje vlastní JavaScript soubor, který webová aplikace načte.

- Stejná pravidla jako pro `registerStyle`.
- `url`: Relativní cesta k JS souboru.

### `createImage(BufferedImage image, String path)`

**Zastaralé (Deprecated)**
Vytvoří obrázek v web-rootu. Doporučuje se používat `getWebRoot()` a standardní Java I/O nebo `AssetStorage`.

### `availableImages()`

**Zastaralé (Deprecated)**
Vrací mapu dostupných obrázků. Doporučuje se používat `getWebRoot()` nebo `AssetStorage`.
