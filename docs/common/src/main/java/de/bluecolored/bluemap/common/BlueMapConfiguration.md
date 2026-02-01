# BlueMapConfiguration.java

## Přehled

`BlueMapConfiguration` je rozhraní definující přístup ke všem konfiguračním částem aplikace BlueMap.

## Umístění

`de.bluecolored.bluemap.common.BlueMapConfiguration`

## Metody

Poskytuje gettery pro:

- `getCoreConfig()`: Hlavní nastavení jádra (vlákna, renderování...).
- `getWebappConfig()`: Nastavení webové aplikace (cesta k webrootu, settings.json...).
- `getWebserverConfig()`: Nastavení integrovaného webserveru (port, bind adresa...).
- `getPluginConfig()`: Nastavení specifická pro plugin (live updates, skiny...).
- `getMapConfigs()`: Mapu konfigurací jednotlivých map.
- `getStorageConfigs()`: Mapu konfigurací úložišť (SQL, File...).
- `getPacksFolder()` / `getModsFolder()`: Cesty ke složkám s resource packy a mody.
- `getMinecraftVersion()`: Konkrétní verze Minecraftu, pro kterou se má BlueMap chovat (nebo null pro autodetekci).