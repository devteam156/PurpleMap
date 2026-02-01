# SpongePlugin.java

## Přehled

`SpongePlugin` je hlavní třída pluginu pro Sponge (entrypoint).

## Umístění

`de.bluecolored.bluemap.sponge.SpongePlugin`

## Implementovaná Rozhraní

`Server`

## Funkcionalita

- **Inicializace (`onServerStart`):**
    - Inicializuje `async` a `sync` exekutory.
    - Spouští pravidelnou úlohu pro aktualizaci hráčů.
    - Spouští asynchronní načítání BlueMap.
    - Registruje eventy a příkazy.
- **Správa hráčů:**
    - Udržuje mapu `onlinePlayerMap` a seznam `onlinePlayerList`.
    - Naslouchá na `ServerSideConnectionEvent` (Join/Leave) a aktualizuje seznamy.
    - `updateSomePlayers` periodicky aktualizuje pozice hráčů.
- **Správa světů:** Udržuje cache `SpongeWorld` instancí.
- **Příkazy:** Registruje příkazy v `onRegisterCommands`.
- **Reload:** Naslouchá na `RefreshGameEvent` (změna konfigurace/reload).

## Metody

### `updateSomePlayers()`

Postupně aktualizuje stavy online hráčů (rozloženo do 20 ticků).
