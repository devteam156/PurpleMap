# LivePlayersDataSupplier.java

## Přehled

`LivePlayersDataSupplier` je `Supplier<String>`, který generuje JSON data o online hráčích pro živou mapu (API endpoint
`/live/players`).

## Umístění

`de.bluecolored.bluemap.common.live.LivePlayersDataSupplier`

## Funkcionalita

- Získá seznam online hráčů ze serveru.
- Aplikuje filtry nastavené v konfiguraci (neviditelnost, sneak, gamemode, jiný svět, úroveň světla).
- Generuje JSON obsahující:
    - UUID, jméno.
    - Pozici (x, y, z).
    - Rotaci (pitch, yaw, roll).
    - Příznak `foreign` (pokud je hráč v jiném světě, než je mapa).

## Použití

Tato třída je registrována v `BlueMapService` nebo webserveru pro obsluhu požadavků na živá data hráčů.