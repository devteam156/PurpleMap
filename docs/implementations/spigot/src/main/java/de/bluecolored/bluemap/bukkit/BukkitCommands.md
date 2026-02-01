# BukkitCommands.java

## Přehled

`BukkitCommands` je třída specifická pro Spigot (kde není Brigadier), která se stará o registraci a zpracování příkazů
BlueMap.

## Umístění

`de.bluecolored.bluemap.bukkit.BukkitCommands`

## Implementovaná Rozhraní

`Listener`

## Funkcionalita

- Používá knihovnu `BlueCommands` pro definici příkazů.
- **CommandProxy:** Vnitřní třída dědící z `BukkitCommand`, která deleguje vykonání příkazu (`execute`) na
  `CommandExecutor`.
- **Tab Complete:** Naslouchá na `TabCompleteEvent`, parsuje vstup a vrací návrhy (completer).
- Řeší registraci příkazů do Bukkit `commandMap` pomocí reflexe (v `BukkitPlugin`).

## Metody

### `getRootCommands()`

Vrátí seznam hlavních příkazů (proxy), které se mají zaregistrovat.

### `onTabComplete(...)`

Zpracovává doplňování příkazů.
