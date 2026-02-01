# SpongeCommandSource.java

## Přehled

`SpongeCommandSource` je implementace `CommandSource` pro Sponge. Obaluje `Audience` a `Subject`.

## Umístění

`de.bluecolored.bluemap.sponge.SpongeCommandSource`

## Implementovaná Rozhraní

`CommandSource`

## Funkcionalita

- **Zprávy:** Posílá zprávy přes `Audience` (Adventure API je v Sponge nativní).
- **Oprávnění:** Kontroluje oprávnění přes `Subject`.
- **Kontext:** Pokud je zdroj `Locatable` (např. hráč), získá pozici a svět.

## Metody

Implementuje metody rozhraní `CommandSource`.
