# Line.java

## Přehled

Třída `Line` reprezentuje lomenou čáru (nebo cestu) v 3D prostoru, složenou ze 2 nebo více bodů (`Vector3d`). Třída je
neměnná (immutable) po vytvoření.

## Umístění

`de.bluecolored.bluemap.api.math.Line`

## Konstruktory

### `Line(Vector3d... points)`

Vytvoří čáru z pole bodů.

- **Výjimky:** `IllegalArgumentException` pokud je počet bodů menší než 2.

### `Line(Collection<Vector3d> points)`

Vytvoří čáru z kolekce bodů.

## Metody

### `getPointCount()`

Vrací počet bodů v čáře.

### `getPoint(int i)`

Vrací bod na daném indexu.

### `getPoints()`

Vrací **kopii** pole bodů.

### `getMin()`

Vypočítá a vrátí minimální bod (souřadnice) ohraničujícího kvádru (AABB). Cachováno.

### `getMax()`

Vypočítá a vrátí maximální bod (souřadnice) ohraničujícího kvádru (AABB). Cachováno.

### `equals(Object o)`

Porovnává čáru s jiným objektem na základě bodů.

### `hashCode()`

Generuje hash kód na základě bodů.

## Statické Metody

### `builder()`

Vrací instanci `Builder` pro vytváření čáry.

## Vnořená třída `Builder`

Pomocná třída pro konstrukci `Line`.

### Metody Builderu

- `addPoint(Vector3d point)`: Přidá jeden bod na konec čáry.
- `addPoints(Vector3d... points)`: Přidá více bodů.
- `addPoints(Collection<Vector3d> points)`: Přidá kolekci bodů.
- `build()`: Vytvoří instanci `Line`. Vyhodí `IllegalStateException`, pokud je méně než 2 body.
