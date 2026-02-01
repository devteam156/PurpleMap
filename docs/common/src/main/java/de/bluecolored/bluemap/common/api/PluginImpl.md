# PluginImpl.java

## Přehled

`PluginImpl` je implementace rozhraní `de.bluecolored.bluemap.api.plugin.Plugin`. Deleguje volání na interní instanci
`de.bluecolored.bluemap.common.plugin.Plugin`.

## Umístění

`de.bluecolored.bluemap.common.api.PluginImpl`

## Implementovaná Rozhraní

`de.bluecolored.bluemap.api.plugin.Plugin`

## Metody

### `getSkinProvider()` / `setSkinProvider(...)`

Získá nebo nastaví `SkinProvider` v `SkinUpdater`u pluginu.

### `getPlayerMarkerIconFactory()` / `setPlayerMarkerIconFactory(...)`

Získá nebo nastaví `PlayerIconFactory` v `SkinUpdater`u pluginu.

### `getPlugin()`

Vrací interní instanci `Plugin`.
