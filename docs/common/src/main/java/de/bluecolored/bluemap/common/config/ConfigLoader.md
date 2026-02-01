# ConfigLoader.java

## Přehled

`ConfigLoader` definuje rozhraní pro různé formáty konfiguračních souborů. BlueMap nativně podporuje HOCON a JSON.

## Umístění

`de.bluecolored.bluemap.common.config.ConfigLoader`

## Implementované Formáty (Registry)

### `HOCON`

- Přípona: `.conf`
- Implementace: `HoconConfigurationLoader`
- **Výchozí formát BlueMap.**

### `JSON`

- Přípona: `.json`
- Implementace: `GsonConfigurationLoader`

## Metody rozhraní

- `getFileSuffix()`: Vrátí příponu souboru (včetně tečky).
- `createLoaderBuilder()`: Vrátí builder pro vytvoření loaderu z knihovny Configurate.

## Vnitřní třída `Impl`

Jednoduchá implementace rozhraní používající `Supplier` pro buildery.