# Player.java

## Přehled

`Player` je abstraktní třída reprezentující hráče na serveru. Slouží jako rozhraní mezi platformě-specifickou
implementací hráče (Bukkit Player, Sponge Player atd.) a společnou logikou BlueMap.

## Umístění

`de.bluecolored.bluemap.common.serverinterface.Player`

## Metody

### `getUuid()`

Vrací unikátní ID hráče (UUID).

### `getName()`

Vrací jméno hráče jako `Text` (formátovaný text).

### `getWorld()`

Vrací svět (`ServerWorld`), ve kterém se hráč právě nachází.

### `getPosition()`

Vrací aktuální pozici hráče (`Vector3d`).

### `getRotation()`

Vrací rotaci (pohled) hráče.

- x -> pitch (sklon)
- y -> yaw (natočení)
- z -> roll (náklon)

### `getSkyLight()` a `getBlockLight()`

Vrací úroveň světla na pozici hráče (pro filtrování viditelnosti ve tmě).

### `isSneaking()`

Vrací `true`, pokud se hráč plíží (sneak).

### `isInvisible()`

Vrací `true`, pokud je hráč neviditelný (efekt lektvaru).

### `isVanished()`

Vrací `true`, pokud je hráč "zmizelý" (vanish) pomocí pluginu. Výchozí implementace vrací `false`, platformy to mohou
přepsat.

### `getGamemode()`

Vrací herní mód hráče (`Gamemode`).

### `equals()` a `hashCode()`

Implementovány na základě UUID hráče.
