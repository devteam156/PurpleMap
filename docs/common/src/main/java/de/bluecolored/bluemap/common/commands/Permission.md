# Permission.java

## Přehled

`Permission` je anotace používaná k označení metod příkazů, které vyžadují specifické oprávnění.

## Umístění

`de.bluecolored.bluemap.common.commands.Permission`

## Použití

`@Permission("bluemap.command.reload")`
public void reload(...) { ... }

Tato anotace je zpracována v `Commands` třídě pomocí predikátu, který volá `commandSource.hasPermission()`.
