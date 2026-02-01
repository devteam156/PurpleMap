# MapSettingsSerializer.java

## Přehled

`MapSettingsSerializer` je `JsonSerializer`, který převádí objekt `BmMap` na JSON objekt obsahující nastavení mapy.
Tento JSON se ukládá do `settings.json` a používá ho webová aplikace.

## Umístění

`de.bluecolored.bluemap.core.map.MapSettingsSerializer`

## Implementovaná Rozhraní

`JsonSerializer<BmMap>`

## Serializovaná data

Vytváří JSON s následujícími klíči:

- `name`: Zobrazované jméno mapy.
- `sorting`: Pořadí řazení.
- `hires`: Nastavení pro high-res dlaždice (velikost dlaždice, měřítko, posun).
- `lowres`: Nastavení pro low-res dlaždice (velikost, LOD faktory).
- `startPos`: Výchozí pozice kamery.
- `skyColor`, `voidColor`: Barvy prostředí.
- `ambientLight`, `skyLight`: Nastavení osvětlení.
- `perspectiveView`, `flatView`, `freeFlightView`: Povolené režimy pohledu.
