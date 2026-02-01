# BukkitCommandSource.java

## Přehled

`BukkitCommandSource` je implementace `CommandSource` pro Paper (pomocí Brigadier API). Obaluje
`io.papermc.paper.command.brigadier.CommandSourceStack`.

## Umístění

`de.bluecolored.bluemap.bukkit.BukkitCommandSource`

## Implementovaná Rozhraní

`CommandSource`

## Funkcionalita

- **Zprávy:** Odesílá zprávy zdroji příkazu.
- **Oprávnění:** Kontroluje oprávnění (`sender.hasPermission`).
- **Kontext:** Poskytuje svět a pozici.
    - Obsahuje workaround pro bug v Paperu, kde `getLocation()` může vyhodit `NullPointerException`.

## Metody

Implementuje metody rozhraní `CommandSource`.
