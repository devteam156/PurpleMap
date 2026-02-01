# SpongePlayer.java

## Přehled

`SpongePlayer` je implementace `Player` pro Sponge. Obaluje
`org.spongepowered.api.entity.living.player.server.ServerPlayer`.

## Umístění

`de.bluecolored.bluemap.sponge.SpongePlayer`

## Dědičnost

`Player` -> `SpongePlayer`

## Funkcionalita

- Poskytuje informace o hráči: UUID, jméno, pozici, rotaci, gamemode.
- Zjišťuje stav efektů (neviditelnost) a `VanishState`.
- Čte úroveň osvětlení na pozici hráče.
- Aktualizuje data v metodě `update()`.

## Metody

Implementuje všechny abstraktní metody třídy `Player` pomocí volání metod na `ServerPlayer`.
