# TileState.java

## Přehled

`TileState` je rozhraní (a registr) definující možné stavy dlaždice a logiku přechodů mezi nimi. Slouží jako stavový
automat pro rozhodování, co se má s dlaždicí stát při aktualizaci mapy.

## Umístění

`de.bluecolored.bluemap.core.map.renderstate.TileState`

## Implementovaná Rozhraní

`Keyed`, `TileActionResolver`

## Stavy (Konstanty)

- `UNKNOWN`: Neznámý stav (výchozí).
- `RENDERED`: Dlaždice je úspěšně vyrenderována.
- `RENDERED_EDGE`: Dlaždice je vyrenderována, ale nachází se na hraně renderovací masky.
- `OUT_OF_BOUNDS`: Dlaždice je mimo hranice mapy (byla smazána).
- `NOT_GENERATED`: Chunk pro tuto dlaždici ještě nebyl vygenerován.
- `MISSING_LIGHT`: Chunku chybí data o osvětlení.
- `LOW_INHABITED_TIME`: Chunk nesplňuje podmínku minimálního času obývání hráči.
- `CHUNK_ERROR`: Chyba při načítání chunku.
- `RENDER_ERROR`: Chyba při renderování.

## Metody

### `findActionAndNextState(boolean changed, BoundsSituation bounds)`

Rozhodne o akci (`RENDER`, `DELETE`, `NONE`) a budoucím stavu dlaždice na základě:

- `changed`: Zda se chunk změnil (hash se liší).
- `bounds`: Pozice dlaždice vůči masce (`INSIDE`, `EDGE`, `OUTSIDE`).

**Příklad logiky:**
Pokud je dlaždice ve stavu `RENDERED` a je stále `INSIDE` masky:

- Pokud se chunk změnil -> Akce `RENDER`, nový stav `RENDERED`.
- Pokud se chunk nezměnil -> Akce `NONE`, stav zůstává `RENDERED`.
  Pokud se maska změnila a dlaždice je nyní `OUTSIDE` -> Akce `DELETE`, nový stav `OUT_OF_BOUNDS`.
