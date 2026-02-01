# ConfigManager.java

## Přehled

`ConfigManager` je nízkoúrovňový nástroj pro práci s konfiguračními soubory. Obaluje knihovnu **Configurate** a
poskytuje jednotné rozhraní pro načítání, parsování a registraci vlastních serializátorů.

## Umístění

`de.bluecolored.bluemap.common.config.ConfigManager`

## Balíček

`de.bluecolored.bluemap.common.config`

## Atributy

- `configRoot`: Cesta k hlavnímu adresáři s konfiguracemi.
- `CONFIG_TEMPLATE_RESOURCE_PATH`: Cesta k resources se šablonami (`/de/bluecolored/bluemap/config/`).

## Metody

### `loadConfig(String name, Class<T> type)`

Vyhledá soubor podle jména (zkouší různé přípony přes `ConfigLoader`), načte ho a převede na instanci třídy `type`.

### `loadConfigTemplate(String name)`

Načte textový obsah šablony z resources aplikace. Šablona je uložena v objektu `ConfigTemplate`.

### `resolveConfigFile(String name)`

Najde existující soubor na disku. Prochází registrované loadery (HOCON, JSON). Pokud žádný soubor nenajde, vrátí cestu s
výchozí příponou `.conf`.

### `loadConfigFile(Path path)` (Privátní)

Vytvoří příslušný `ConfigurationLoader`, načte uzel (`ConfigurationNode`) a ošetří chyby při čtení nebo syntaxi.

### `getLoader(Path path)` (Privátní)

Vytvoří a nakonfiguruje builder pro `ConfigurationLoader`.

- **Custom Serializers:** Registruje vlastní serializátory pro typy:
    - `Vector2i`, `Vector2d` (matematické vektory).
    - `Key` (BlueMap identifikátory).
    - `CombinedMask` (složené renderovací masky).
    - `StorageConfig`, `MaskConfig` (používá `ObjectMapperSerializer` pro polymorfní typy).

### `getConfigName(Path file)`

Získá čistý název konfigurace odstraněním přípony (např. `core.conf` -> `core`).