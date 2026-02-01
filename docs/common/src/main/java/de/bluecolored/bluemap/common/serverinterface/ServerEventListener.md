# ServerEventListener.java

## Přehled

`ServerEventListener` je rozhraní pro naslouchání událostem serveru, které jsou relevantní pro BlueMap.

## Umístění

`de.bluecolored.bluemap.common.serverinterface.ServerEventListener`

## Metody

### `onPlayerJoin(UUID playerUuid)`

Volá se, když se hráč připojí na server.

### `onPlayerLeave(UUID playerUuid)`

Volá se, když se hráč odpojí ze serveru.
