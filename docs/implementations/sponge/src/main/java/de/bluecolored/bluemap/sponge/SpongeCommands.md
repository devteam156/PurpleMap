# SpongeCommands.java

## Přehled

`SpongeCommands` spravuje registraci a zpracování příkazů pro Sponge API.

## Umístění

`de.bluecolored.bluemap.sponge.SpongeCommands`

## Funkcionalita

- Vytváří příkazovou strukturu pomocí `Commands.create`.
- **SpongeCommandProxy:** Vnitřní třída implementující `org.spongepowered.api.command.Command.Raw`, která slouží jako
  adaptér mezi Sponge příkazovým systémem a `BlueCommands`.
- Zajišťuje zpracování příkazů (`process`) a doplňování tabulátorem (`complete`).

## Metody

### `getRootCommands()`

Vrátí seznam proxy příkazů k registraci.
