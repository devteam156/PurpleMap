# ForgeMod.java

## Přehled

`ForgeMod` je hlavní třída módu pro Forge (označená `@Mod`).

## Umístění

`de.bluecolored.bluemap.forge.ForgeMod`

## Implementovaná Rozhraní

`Server`

## Funkcionalita

- **Inicializace:** Registruje se na event bus, inicializuje `BlueMapService` a `Plugin`.
- **Eventy:** Naslouchá na události serveru (`ServerStartingEvent`, `ServerStartedEvent`, `ServerStoppingEvent`,
  `RegisterCommandsEvent`) a hráčů (`PlayerLoggedInEvent`, `PlayerLoggedOutEvent`).
- **Příkazy:** Registruje příkazy BlueMap pomocí Brigadier.
- **Update Hráčů:** V `onTick` (ServerTickEvent) aktualizuje pozice online hráčů pro živou mapu (postupně, aby
  nezatěžoval server).
- **Kompatibilita:** Registruje `DisplayTest.IGNORESERVERONLY`, aby se klienti mohli připojit i bez nainstalovaného
  módu.

## Metody

### `onRegisterCommands(...)`

Registruje příkazy.

### `onServerStarted(...)`

Spustí načítání BlueMap v novém vlákně. Uloží chunky (`saveAllChunks`) pro vygenerování `level.dat`.

### `updateSomePlayers()`

Rozkládá aktualizaci hráčů do více ticků.
