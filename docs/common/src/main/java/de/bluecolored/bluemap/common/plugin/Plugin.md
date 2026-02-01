# Plugin.java

## Přehled

Třída `Plugin` (v balíčku `common`) představuje jádro logiky, která je společná pro všechny serverové implementace (
Spigot, Fabric, Forge, atd.). Nejedná se o API rozhraní `Plugin`, ale o hlavní řídící třídu.

## Umístění

`de.bluecolored.bluemap.common.plugin.Plugin`

## Implementovaná Rozhraní

`ServerEventListener`

## Hlavní komponenty

- `BlueMapService`: Správa konfigurace a zdrojů.
- `RenderManager`: Správa renderování.
- `HttpServer`: Interní webserver.
- `PluginState`: Ukládání stavu (např. zmrazené mapy).
- `BlueMapAPIImpl`: Implementace veřejného API.
- `MapUpdateService`: Sledování změn souborů.

## Metody

### `load()` / `load(ResourcePack preloaded)`

Načte a inicializuje celý plugin.

- Načte konfigurace a addony.
- Inicializuje `BlueMapService`.
- Spustí webserver (pokud je povolen).
- Inicializuje `RenderManager` a plánovače úloh.
- Zaregistruje API.
- Spustí sledování změn v mapách.

### `unload()`

Ukončí činnost pluginu, zastaví servery, vlákna a uvolní zdroje.

### `reload()`

Provede `unload()` a následně `load()`.

### `lightReload()`

Provede reload, ale pokusí se zachovat načtený resource pack (což je časově nejnáročnější operace).

### `save()`

Uloží stav pluginu (`pluginState.json`) a stav všech map.

### `startWatchingMap(BmMap map)` / `stopWatchingMap(BmMap map)`

Spustí nebo zastaví `MapUpdateService` pro danou mapu.

### `checkPausedByPlayerCount()`

Zkontroluje, zda počet online hráčů nepřekračuje limit (`playerRenderLimit`). Pokud ano, pozastaví renderer.
