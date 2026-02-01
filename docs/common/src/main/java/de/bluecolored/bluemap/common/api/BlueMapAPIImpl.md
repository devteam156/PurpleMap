# BlueMapAPIImpl.java

## Přehled

`BlueMapAPIImpl` je implementace abstraktní třídy `BlueMapAPI`. Představuje most mezi veřejným API a vnitřní logikou
BlueMap (reprezentovanou `BlueMapService` a `Plugin`).

## Umístění

`de.bluecolored.bluemap.common.api.BlueMapAPIImpl`

## Dědičnost

`BlueMapAPI` -> `BlueMapAPIImpl`

## Konstruktory

### `BlueMapAPIImpl(Plugin plugin)`

Vytvoří implementaci API pro daný plugin. Automaticky získá `BlueMapService` z pluginu.

### `BlueMapAPIImpl(BlueMapService blueMapService, Plugin plugin)`

Vytvoří implementaci API s explicitní službou a volitelným pluginem.

## Metody

### `getMaps()`

Vrací kolekci `BlueMapMap` objektů. Mapy jsou získány z `BlueMapService` a zabaleny do API implementace (
`BlueMapMapImpl`).

### `getWorlds()`

Vrací kolekci `BlueMapWorld` objektů. Světy jsou získány z `BlueMapService` a zabaleny do API implementace (
`BlueMapWorldImpl`).

### `getWorld(Object world)`

Získá svět pomocí cache (`worldCache`). Podporuje různé typy identifikátorů (String ID, World objekt z jádra, objekt
světa ze serverového rozhraní).

### `getMap(String id)`

Získá mapu podle ID pomocí cache (`mapCache`).

### `getWebApp()`

Vrací implementaci `WebAppImpl`.

### `getRenderManager()`

Vrací implementaci `RenderManagerImpl`. Pokud není k dispozici plugin (např. v CLI), vyhodí výjimku.

### `getPlugin()`

Vrací implementaci `PluginImpl`. Pokud není k dispozici plugin, vyhodí výjimku.

### `register()`

Zaregistruje tuto instanci jako globální instanci API (`BlueMapAPI.getInstance()`).

### `unregister()`

Odregistruje tuto instanci.

### `blueMapService()` a `plugin()`

Pomocné metody pro přístup k interním objektům `BlueMapService` a `Plugin`. Užitečné pro addony, které závisí na
`BlueMapCommon`.
