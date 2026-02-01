# CommandSource.java

## Přehled

`CommandSource` je rozhraní, které abstrahuje zdroj příkazu (hráče, konzoli, command block) napříč různými platformami (
Bukkit, Sponge, Fabric, atd.).

## Umístění

`de.bluecolored.bluemap.common.serverinterface.CommandSource`

## Metody

### `sendMessage(Component text)`

Pošle zprávu zdroji příkazu. Používá Adventure API (`Component`).

### `hasPermission(String permission)`

Zkontroluje, zda má zdroj příkazu dané oprávnění.

### `getWorld()`

Vrátí `Optional<ServerWorld>`, ve kterém se zdroj příkazu nachází (pokud je to hráč nebo entita).

### `getPosition()`

Vrátí `Optional<Vector3d>`, kde se zdroj příkazu nachází.
