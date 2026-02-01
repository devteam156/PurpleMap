# BlueMapConfigManager.java

## Přehled

`BlueMapConfigManager` je hlavní implementace rozhraní `BlueMapConfiguration`. Zodpovídá za koordinované načítání všech
konfiguračních souborů, jejich inicializaci (včetně vytváření výchozích souborů ze šablon) a správu mapových a úložných
konfigurací.

## Umístění

`de.bluecolored.bluemap.common.config.BlueMapConfigManager`

## Balíček

`de.bluecolored.bluemap.common.config`

## Implementovaná Rozhraní

- `BlueMapConfiguration`

## Atributy

### Statické Konstanty (Názvy souborů/složek)

- `CORE_CONFIG_NAME`: "core"
- `WEBSERVER_CONFIG_NAME`: "webserver"
- `WEBAPP_CONFIG_NAME`: "webapp"
- `PLUGIN_CONFIG_NAME`: "plugin"
- `MAPS_CONFIG_FOLDER_NAME`: "maps"
- `STORAGES_CONFIG_FOLDER_NAME`: "storages"

### Instance Konfigurací

- `configManager`: `ConfigManager` - nástroj pro samotné načítání a parsování.
- `coreConfig`: Hlavní nastavení jádra.
- `webserverConfig`: Nastavení HTTP serveru.
- `webappConfig`: Nastavení webového klienta.
- `pluginConfig`: Nastavení specifická pro integraci do Minecraftu.
- `mapConfigs`: Mapa ID mapy -> `MapConfig`.
- `storageConfigs`: Mapa ID úložiště -> `StorageConfig`.

## Konstruktor (Lombok `@Builder`)

Konstruktor provádí sekvenční načítání všech částí systému. Pokud konfigurační soubory neexistují, automaticky je
vytvoří ze šablon s vyplněnými proměnnými.

**Logika inicializace:**

1. Nastavení výchozích cest pro data a webroot (pokud nejsou zadány).
2. Inicializace `ConfigManager`u.
3. Postupné volání `load...Config` metod.
4. **Auto-konfigurace světů:** Pokud jsou předány instance `ServerWorld` a neexistují žádné konfigurace map, manažer
   automaticky vygeneruje konfigurace pro overworld, nether a end.

## Vnitřní Metody (Načítání konfigurací)

### `loadCoreConfig(...)`

Načte `core.conf`. Pokud chybí:

- Vypočítá doporučený počet renderovacích vláken (`suggestRenderThreadCount`) na základě CPU a paměti.
- Použije šablonu a dosadí proměnné jako `version`, `mcVersion`, `data` cestu atd.
- Uloží výchozí soubor a pak ho načte.

### `loadMapConfigs(...)`

Načítá soubory ze složky `maps/`.

- Podporuje automatickou detekci map pro existující světy na serveru.
- Generuje unikátní ID mapy očištěním názvu světa a dimenze (`sanitiseMapId`).
- Pro každý soubor v adresáři ověří integritu a unikátnost ID.

### `loadStorageConfigs(...)`

Načítá definice úložišť ze složky `storages/`.

- Ve výchozím stavu vytvoří šablony pro `file` (souborové) a `sql` úložiště.
- Při načítání nejdříve zjistí typ úložiště a poté znovu načte soubor s konkrétní třídou nastavení (např. `SQLConfig`).

## Pomocné Metody

### `suggestRenderThreadCount()`

- **Logika:**
    - 6+ jader a 4GB RAM -> 2 vlákna.
    - 10+ jader a 8GB RAM -> 3 vlákna.
    - Jinak 1 vlákno (pesimistický odhad pro stabilitu).

### `formatPath(Path path)`

Normalizuje cestu pro zápis do konfiguračních souborů. Nahrazuje systémové oddělovače dopřednými lomítky a escapuje
zpětná lomítka (`\ -> \\`).

### `sanitiseMapId(String id)`

Nahrazuje všechny nealfanumerické znaky podtržítkem (`\W -> _`).