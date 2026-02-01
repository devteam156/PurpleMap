# Shape.java

## Přehled

Třída `Shape` reprezentuje geometrický útvar (tvar) na 2D rovině, definovaný sadou bodů (`Vector2d`). Tvar musí mít
alespoň 3 body. Třída je navržena jako neměnná (immutable) po svém vytvoření (kromě líné inicializace min/max hodnot).

## Umístění

`de.bluecolored.bluemap.api.math.Shape`

## Konstruktory

### `Shape(Vector2d... points)`

Vytvoří tvar z pole bodů.

- **Výjimky:** `IllegalArgumentException` pokud je počet bodů menší než 3.

### `Shape(Collection<Vector2d> points)`

Vytvoří tvar z kolekce bodů.

## Metody

### `getPointCount()`

Vrací počet bodů, které tvoří tento tvar.

### `getPoint(int i)`

Vrací bod na zadaném indexu `i`.

### `getPoints()`

Vrací **kopii** pole bodů tvořících tento tvar.

### `getMin()`

Vypočítá a vrátí minimální roh (souřadnice) axis-aligned bounding boxu (AABB) tohoto tvaru. Hodnota je cachována (
lazy-loaded).

### `getMax()`

Vypočítá a vrátí maximální roh (souřadnice) axis-aligned bounding boxu (AABB) tohoto tvaru. Hodnota je cachována (
lazy-loaded).

### `equals(Object o)`

Porovnává tento tvar s jiným objektem na základě rovnosti bodů.

### `hashCode()`

Vrací hash kód založený na bodech tvaru.

## Statické Metody (Tovární metody)

### `createRect(Vector2d pos1, Vector2d pos2)`

Vytvoří obdélníkový tvar definovaný dvěma protilehlými rohy.

### `createRect(double x1, double y1, double x2, double y2)`

Vytvoří obdélníkový tvar pomocí souřadnic dvou protilehlých rohů.

### `createEllipse(Vector2d centerPos, double radiusX, double radiusY, int points)`

Vytvoří tvar elipsy.

- `centerPos`: Střed elipsy.
- `radiusX`: Poloměr v ose X.
- `radiusY`: Poloměr v ose Y.
- `points`: Počet bodů, které budou elipsu aproximovat (musí být >= 3).

### `createEllipse(double centerX, double centerY, double radiusX, double radiusY, int points)`

Vytvoří tvar elipsy pomocí souřadnic středu.

### `createCircle(Vector2d centerPos, double radius, int points)`

Vytvoří tvar kruhu (speciální případ elipsy, kde poloměr X a Y jsou shodné).

### `createCircle(double centerX, double centerY, double radius, int points)`

Vytvoří tvar kruhu pomocí souřadnic středu.

### `builder()`

Vrací instanci `Builder` pro postupné vytváření tvaru.

## Vnořená třída `Builder`

Pomocná třída pro vytváření instancí `Shape`.

### Metody Builderu

- `addPoint(Vector2d point)`: Přidá bod.
- `addPoints(Vector2d... points)`: Přidá pole bodů.
- `addPoints(Collection<Vector2d> points)`: Přidá kolekci bodů.
- `build()`: Vytvoří instanci `Shape`. Vyhodí `IllegalStateException`, pokud je přidáno méně než 3 body.
