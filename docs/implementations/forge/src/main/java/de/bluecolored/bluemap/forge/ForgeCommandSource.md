# ForgeCommandSource.java

## Přehled

`ForgeCommandSource` je implementace `CommandSource` pro Forge. Obaluje `net.minecraft.commands.CommandSourceStack`.

## Umístění

`de.bluecolored.bluemap.forge.ForgeCommandSource`

## Implementovaná Rozhraní

`CommandSource`

## Funkcionalita

- **Zprávy:** Převádí a posílá zprávy zdroji příkazu.
- **Oprávnění:** Kontroluje oprávnění pomocí vanilla systému (`delegate.hasPermission(2)`).
- **Kontext:** Poskytuje svět a pozici, odkud byl příkaz vykonán.
