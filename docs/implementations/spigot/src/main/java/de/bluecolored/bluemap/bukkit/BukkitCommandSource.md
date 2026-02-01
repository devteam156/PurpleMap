# BukkitCommandSource.java

## Přehled

`BukkitCommandSource` je implementace `CommandSource` pro Spigot. Obaluje `org.bukkit.command.CommandSender`.

## Umístění

`de.bluecolored.bluemap.bukkit.BukkitCommandSource`

## Implementovaná Rozhraní

`CommandSource`

## Funkcionalita

- **Zprávy:** Převádí Adventure `Component` na BungeeCord Chat API (používané ve Spigotu) a odesílá zprávu.
- **Oprávnění:** Kontroluje oprávnění (`sender.hasPermission`).
- **Kontext:**
    - Pokud je sender `Entity`, získá jeho pozici a svět.
    - Pokud je sender `BlockCommandSender` (command block), získá jeho pozici a svět.
    - Jinak (konzole) vrací prázdné Optional.

## Metody

Implementuje metody rozhraní `CommandSource`.
