# WebAppImpl.java

## Přehled

`WebAppImpl` implementuje rozhraní `WebApp`. Zajišťuje propojení API pro webovou aplikaci se zbytkem systému (
konfigurací, souborovým manažerem, stavem pluginu).

## Umístění

`de.bluecolored.bluemap.common.api.WebAppImpl`

## Implementovaná Rozhraní

`WebApp`

## Konstruktory

### `WebAppImpl(BlueMapService blueMapService, Plugin plugin)`

Vytvoří instanci pro danou službu a plugin.

### `WebAppImpl(Plugin plugin)`

Alternativní konstruktor, který si vytáhne službu z pluginu.

## Metody

### `getWebRoot()`

Vrátí cestu k webrootu z aktuální konfigurace.

### `setPlayerVisibility(UUID player, boolean visible)`

Mění viditelnost hráče v `PluginState`. Pokud plugin není přítomen (např. CLI), metoda nic nedělá.

### `getPlayerVisibility(UUID player)`

Zjišťuje viditelnost hráče z `PluginState`.

### `registerScript(String url)`

Přidá URL skriptu do `WebFilesManager`u a naplánuje uložení nastavení (`settings.json`).

### `registerStyle(String url)`

Přidá URL stylu (CSS) do `WebFilesManager`u a naplánuje uložení nastavení.

### `scheduleUpdateWebAppSettings()`

Privátní metoda, která pomocí časovače (`Timer`) odloží uložení `settings.json` o 1 sekundu. To slouží k optimalizaci (
debounce) při hromadné registraci více skriptů/stylů najednou, aby se soubor nepřepisoval opakovaně.

### `createImage(...)` a `availableImages()`

Implementace zastaralých metod pro práci s obrázky. `createImage` fyzicky zapíše obrázek na disk do
`webroot/data/images`.
