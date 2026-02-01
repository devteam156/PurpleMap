# ShapeMarker.java

## Přehled

`ShapeMarker` je typ markeru, který zobrazuje geometrický útvar (tvar) na mapě. Dědí z `ObjectMarker`. Tvar je definován
na rovině XZ a umístěn v určité výšce Y. Marker může mít volitelnou barvu výplně a obrysu, a může obsahovat díry.

## Umístění

`de.bluecolored.bluemap.api.markers.ShapeMarker`

## Dědičnost

`DistanceRangedMarker` -> `ObjectMarker` -> `ShapeMarker`

## Konstruktory

### `ShapeMarker(String label, Shape shape, float shapeY)`

Vytvoří nový `ShapeMarker`. Pozice markeru (pro účely zobrazení štítku a vzdálenosti) bude automaticky nastavena na
střed bounding boxu tvaru.

- `label`: Popisek markeru.
- `shape`: Tvar markeru (`Shape`).
- `shapeY`: Výška (Y-souřadnice), ve které se tvar vykreslí.

### `ShapeMarker(String label, Vector3d position, Shape shape, float shapeY)`

Vytvoří nový `ShapeMarker` s explicitně definovanou pozicí.

- `position`: Pozice markeru (např. pro zobrazení štítku).

## Metody

### `getShape()`

Vrací tvar (`Shape`) tohoto markeru.

### `getShapeY()`

Vrací výšku (Y), ve které je tvar vykreslen.

### `setShape(Shape shape, float y)`

Nastaví nový tvar a jeho výšku.

### `getHoles()`

Vrací **měnitelnou** kolekci tvarů (`Collection<Shape>`), které představují díry v hlavním tvaru.

### `centerPosition()`

Přepočítá a nastaví pozici markeru na střed bounding boxu aktuálního tvaru.

### `isDepthTestEnabled()` / `setDepthTestEnabled(boolean enabled)`

Určuje, zda se má při vykreslování provádět depth-test. Pokud je vypnutý (`false`), marker bude viditelný i přes jiné
objekty (zdi, terén).

### `getLineWidth()` / `setLineWidth(int width)`

Získá nebo nastaví šířku obrysové čáry v pixelech.

### `getLineColor()` / `setLineColor(Color color)`

Získá nebo nastaví barvu obrysové čáry.

### `getFillColor()` / `setFillColor(Color color)`

Získá nebo nastaví barvu výplně tvaru.

### `setColors(Color lineColor, Color fillColor)`

Pohodlná metoda pro nastavení barvy obrysu i výplně najednou.

### `builder()`

Vrací `Builder` pro vytváření instancí `ShapeMarker`.

## Vnořená třída `Builder`

Umožňuje plynulé vytváření `ShapeMarker`.

### Metody Builderu

- `shape(Shape shape, float y)`: Nastaví tvar a výšku.
- `holes(Shape... holes)`: Přidá díry do tvaru.
- `clearHoles()`: Odstraní všechny díry.
- `centerPosition()`: Nastaví, aby se pozice vypočítala automaticky ze středu tvaru.
- `depthTestEnabled(boolean enabled)`: Nastaví depth-test.
- `lineWidth(int width)`: Nastaví šířku čáry.
- `lineColor(Color color)`: Nastaví barvu čáry.
- `fillColor(Color color)`: Nastaví barvu výplně.
- `build()`: Vytvoří instanci `ShapeMarker`. Vyžaduje nastavený `label` a `shape`.
