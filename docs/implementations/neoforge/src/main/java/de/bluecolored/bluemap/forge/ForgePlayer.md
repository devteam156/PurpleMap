# ForgePlayer.java

## Přehled

`ForgePlayer` je implementace `Player` pro NeoForge. Obaluje `net.minecraft.server.level.ServerPlayer`.

## Umístění

`de.bluecolored.bluemap.forge.ForgePlayer`

## Dědičnost

`Player` -> `ForgePlayer`

## Funkcionalita

- Poskytuje informace o hráči pro BlueMap (UUID, jméno, pozici, rotaci, gamemode).
- Zjišťuje stav efektů (neviditelnost) a plížení.
- Čte úroveň osvětlení na pozici hráče.
- Aktualizuje data v metodě `update()`.

## Metody

Implementuje všechny abstraktní metody třídy `Player` pomocí volání metod na `ServerPlayer`.
