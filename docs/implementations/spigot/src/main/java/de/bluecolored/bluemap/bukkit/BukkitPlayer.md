# BukkitPlayer.java

## Přehled

`BukkitPlayer` je implementace `Player` pro Spigot/Bukkit. Obaluje `org.bukkit.entity.Player`.

## Umístění

`de.bluecolored.bluemap.bukkit.BukkitPlayer`

## Dědičnost

`Player` -> `BukkitPlayer`

## Funkcionalita

- Poskytuje informace o hráči: UUID, jméno, pozici, rotaci, gamemode.
- Zjišťuje stav efektů (neviditelnost) a metadat (vanish).
- Čte úroveň osvětlení na pozici hráče.
- Aktualizuje data v metodě `update()`.

## Metody

Implementuje všechny abstraktní metody třídy `Player` pomocí volání metod na `org.bukkit.entity.Player`.
