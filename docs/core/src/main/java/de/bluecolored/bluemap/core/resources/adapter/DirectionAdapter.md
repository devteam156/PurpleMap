# DirectionAdapter.java

## Přehled

`DirectionAdapter` je GSON adaptér pro `Direction` enum (směry jako NORTH, SOUTH, UP, DOWN...).

## Umístění

`de.bluecolored.bluemap.core.resources.adapter.DirectionAdapter`

## Dědičnost

`TypeAdapter<Direction>` -> `DirectionAdapter`

## Funkcionalita

- **Čtení:** Přečte řetězec a převede ho na `Direction`.
    - Podporuje aliasy "bottom" -> DOWN a "top" -> UP (časté v modelech).
- **Zápis:** Zapíše název směru malými písmeny.
