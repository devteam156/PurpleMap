# LowresTile.java

## Přehled

`LowresTile` reprezentuje jednu dlaždici v low-res (přehledové) mapě. Fyzicky je to obrázek (PNG), kde každý pixel
odpovídá určité oblasti bloků ve světě (v závislosti na LOD úrovni).

## Umístění

`de.bluecolored.bluemap.core.map.lowres.LowresTile`

## Atributy

- `texture`: `BufferedImage`, který uchovává data dlaždice.
    - Horní polovina obrázku obsahuje barvu (RGB).
    - Dolní polovina obrázku kóduje metadata: výšku a úroveň světla.
- `size`: Velikost dlaždice (plus 1 pixel pro bezešvé okraje).
- `lock`: `ReentrantReadWriteLock` pro zajištění thread-safety při zápisu a čtení.

## Metody

### `LowresTile(Vector2i tileSize)`

Vytvoří novou prázdnou dlaždici.

### `LowresTile(Vector2i tileSize, InputStream in)`

Načte dlaždici z proudu (obvykle PNG souboru).

### `set(int x, int z, Color color, int height, int blockLight)`

Zapíše hodnotu pixelu na dané souřadnice.

- Barva se zapíše do horní poloviny textury.
- Výška a světlo se zakódují do dolní poloviny textury.

### `getColor(...)`

Přečte barvu pixelu.

### `getHeight(...)`

Přečte a dekóduje výšku pixelu.

### `getBlockLight(...)`

Přečte a dekóduje úroveň světla.

### `save(OutputStream out)`

Uloží dlaždici jako PNG obrázek do výstupního proudu.
