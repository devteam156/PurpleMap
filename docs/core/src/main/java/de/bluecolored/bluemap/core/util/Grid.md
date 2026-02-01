# Grid.java

## Přehled

`Grid` je klíčová matematická třída pro transformaci souřadnic mezi různými mřížkami (např. z bloků na chunky, z chunků
na regiony). Umožňuje definovat velikost buňky a volitelný offset.

## Umístění

`de.bluecolored.bluemap.core.util.Grid`

## Atributy

- `gridSize`: `Vector2i` - Velikost buňky mřížky (šířka, délka).
- `offset`: `Vector2i` - Posun počátku mřížky.

## Výpočty a Logika

### `getCell(Vector2i pos)`

- **Vzorec:** `floor((pos - offset) / gridSize)`
- **Význam:** Převede absolutní souřadnici na index buňky v mřížce.

### `getLocal(Vector2i pos)`

- **Vzorec:** `(pos - offset) mod gridSize`
- **Význam:** Zjistí relativní pozici bodu v rámci jedné buňky.

### `getCellMin(Vector2i cell)`

- **Vzorec:** `cell * gridSize + offset`
- **Význam:** Vrátí souřadnici levého horního rohu (minimum) dané buňky.

### `getCellMax(Vector2i cell)`

- **Vzorec:** `(cell + 1) * gridSize + offset - 1`
- **Význam:** Vrátí souřadnici pravého dolního rohu (maximum) buňky.

### `multiply(Grid other)`

- **Logika:** Vytvoří novou mřížku, která je součinem dvou mřížek. Např. mřížka chunků (16) * mřížka regionů (32) =
  mřížka regionů v blocích (512).

### `getIntersecting(Vector2i cell, Grid targetGrid)`

- **Význam:** Zjistí, které buňky v cílové mřížce (`targetGrid`) se překrývají s danou buňkou v této mřížce. Používá se
  např. pro zjištění, které dlaždice mapy patří do jednoho regionu.
