# BrigadierExecutionHandler.java

## Přehled

`BrigadierExecutionHandler` rozšiřuje `CommandExecutor` a implementuje rozhraní `CommandExecutionHandler` z knihovny
`BlueCommands` (pro integraci s Brigadierem).

## Umístění

`de.bluecolored.bluemap.common.commands.BrigadierExecutionHandler`

## Dědičnost

`CommandExecutor` -> `BrigadierExecutionHandler`

## Funkcionalita

- **Adaptér pro Brigadier:** Umožňuje použít logiku `CommandExecutor` přímo v Brigadier příkazech.
- **Zpracování chyb parsování:** Pokud `ExecutionResult` indikuje chybu parsování, vyhodí `CommandSyntaxException`, aby
  Brigadier mohl zobrazit správnou chybovou hlášku uživateli (např. "Unknown command").
