# Gamemode.java

## Přehled

`Gamemode` je výčet (enum) herních režimů v Minecraftu. Používá se pro filtrování hráčů na mapě (např. skrytí
spectatorů).

## Umístění

`de.bluecolored.bluemap.common.serverinterface.Gamemode`

## Hodnoty

- `SURVIVAL` ("survival")
- `CREATIVE` ("creative")
- `ADVENTURE` ("adventure")
- `SPECTATOR` ("spectator")

## Metody

### `getId()`

Vrací textové ID herního módu.

### `getById(String id)`

Statická metoda pro získání `Gamemode` podle ID. Pokud ID neexistuje, vyhodí `IllegalArgumentException`.
