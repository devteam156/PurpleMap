# WithPosition.java

## Přehled

`WithPosition` je anotace označující příkazy, které vyžadují, aby měl `CommandSource` (zdroj příkazu) pozici. Typicky se
jedná o příkazy spuštěné hráčem nebo command blockem.

## Umístění

`de.bluecolored.bluemap.common.commands.WithPosition`

## Použití

Tato anotace je zpracována v `Commands.java` při registraci příkazů. Pokud má metoda tuto anotaci, přidá se podmínka (
context predicate), která ověřuje `commandSource.getPosition().isPresent()`. Pokud zdroj pozici nemá (např. konzole),
příkaz nebude pro tento zdroj viditelný nebo spustitelný.
