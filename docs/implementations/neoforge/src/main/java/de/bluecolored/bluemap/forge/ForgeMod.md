# ForgeMod.java

## Přehled

`ForgeMod` je hlavní třída módu pro NeoForge (označená `@Mod`).

## Umístění

`de.bluecolored.bluemap.forge.ForgeMod`

## Implementovaná Rozhraní

`Server`

## Funkcionalita

- **Inicializace:** Registruje se na event bus (NeoForge), inicializuje `BlueMapService` a `Plugin`.
- **Eventy:** Naslouchá na události serveru (`ServerStartingEvent`, `ServerStartedEvent`, `ServerStoppingEvent`,
  `RegisterCommandsEvent`) a hráčů (`PlayerLoggedInEvent`, `PlayerLoggedOutEvent` z balíčku
  `net.neoforged.neoforge.event.entity.player`).
- **Příkazy:** Registruje příkazy BlueMap pomocí Brigadier.
- **Update Hráčů:** V `onTick` (`ServerTickEvent.Post`) aktualizuje pozice online hráčů pro živou mapu (postupně).

## Rozdíly oproti Forge

- Používá `net.neoforged` API.
- Používá `NeoForge.EVENT_BUS` místo `MinecraftForge.EVENT_BUS`.
- Jiné názvy eventů (např. `ServerTickEvent.Post`).

## Metody

### `onRegisterCommands(...)`

Registruje příkazy.

### `onServerStarted(...)`

Spustí načítání BlueMap v novém vlákně. Uloží chunky (`saveAllChunks`) pro vygenerování `level.dat`.

### `updateSomePlayers()`

Rozkládá aktualizaci hráčů do více ticků.
