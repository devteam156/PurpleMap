# Unloaded.java

## Přehled

`Unloaded` je značkovací anotace (marker interface), která označuje příkazy, které lze spustit i v případě, že jádro
BlueMap není plně načtené.

## Umístění

`de.bluecolored.bluemap.common.commands.Unloaded`

## Použití

Používá se v metodách tříd příkazů (např. `ReloadCommand`). Pokud metoda příkazu **nemá** tuto anotaci,
`CommandExecutor` před spuštěním zkontroluje, zda je plugin načten (`plugin.isLoaded()`), a pokud ne, spuštění
zablokuje.
