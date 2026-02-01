# BukkitPlugin.java

## Přehled

`BukkitPlugin` je hlavní třída pluginu pro Spigot (entrypoint).

## Umístění

`de.bluecolored.bluemap.bukkit.BukkitPlugin`

## Implementovaná Rozhraní

`Server`, `Listener`

## Funkcionalita

- **Inicializace (`onEnable`):**
    - Uloží světy (pro vygenerování level.dat).
    - Registruje eventy a forwarder.
    - Registruje příkazy: Protože Spigot nepoužívá Brigadier (jako Paper), používá se vlastní implementace
      `BukkitCommands`, která se injektuje do `commandMap` pomocí reflexe.
    - Spouští asynchronní načítání BlueMap.
    - Startuje bStats.
    - Spouští timer (`updateSomePlayers`) pro aktualizaci pozic hráčů.
- **Správa hráčů:** Udržuje seznam online hráčů a jejich `BukkitPlayer` instancí.
- **Detekce verze:** Snaží se detekovat verzi Minecraftu z `Bukkit.getVersion()`.

## Metody

### `updateSomePlayers()`

Postupně aktualizuje stavy online hráčů (rozloženo do 20 ticků).
