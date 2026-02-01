# GrassColorModifier.java

## Přehled

`GrassColorModifier` je specializovaný `ColorModifier` pro úpravu barvy trávy. Používá se v biomech, které mají
speciální pravidla pro barvu trávy (např. bažiny nebo temné lesy).

## Umístění

`de.bluecolored.bluemap.core.world.biome.GrassColorModifier`

## Implementovaná Rozhraní

`Keyed`, `ColorModifier`

## Konstanty / Registry

- `NONE`: Žádná úprava.
- `DARK_FOREST`: Zprůměruje barvu s tmavou zelenou.
- `SWAMP`: Nastaví barvu na bažinovou zelenou (s případným šumem, který zde není plně implementován).

## Metody

Deleguje na vnitřní `ColorModifier`.
