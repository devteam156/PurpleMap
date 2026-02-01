# FileMapStorage.java

## Přehled

`FileMapStorage` je implementace `MapStorage`, která spravuje data pro jednu konkrétní mapu v souborovém systému.

## Umístění

`de.bluecolored.bluemap.core.storage.file.FileMapStorage`

## Implementovaná Rozhraní

`MapStorage`

## Struktura adresářů

- `tiles/0/`: High-res dlaždice.
- `tiles/<LOD>/`: Low-res dlaždice (např. `tiles/1/`).
- `rstate/`: Stav renderování (dlaždice, chunky).
- `assets/`: Assety mapy.
- `live/`: Živá data (hráči, markery).
- `settings.json`: Nastavení mapy.
- `textures.json`: Mapování textur.

## Metody

Vrací instance `GridStorage` nebo `ItemStorage` pro jednotlivé části dat.
