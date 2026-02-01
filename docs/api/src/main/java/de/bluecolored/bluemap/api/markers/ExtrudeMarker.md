# ExtrudeMarker.java

## Přehled

`ExtrudeMarker` je podobný `ShapeMarker`u, ale umožňuje vytáhnout (extrudovat) 2D tvar do výšky, čímž vznikne 3D
těleso (hranol) na mapě. Definuje se tvarem na rovině XZ a minimální a maximální výškou Y.

## Umístění

`de.bluecolored.bluemap.api.markers.ExtrudeMarker`

## Dědičnost

`ObjectMarker` -> `ExtrudeMarker`

## Konstruktory

### `ExtrudeMarker(String label, Shape shape, float shapeMinY, float shapeMaxY)`

Vytvoří nový `ExtrudeMarker`. Pozice se automaticky nastaví na střed tělesa.

- `label`: Popisek.
- `shape`: 2D tvar podstavy.
- `shapeMinY`: Spodní výška (Y).
- `shapeMaxY`: Horní výška (Y).

### `ExtrudeMarker(String label, Vector3d position, Shape shape, float shapeMinY, float shapeMaxY)`

Vytvoří nový `ExtrudeMarker` s explicitní pozicí.

## Metody

### `getShape()` / `setShape(Shape shape, float minY, float maxY)`

Získá tvar podstavy nebo nastaví nový tvar a výškové rozpětí.

### `getShapeMinY()`

Vrací spodní výšku extrudovaného tvaru.

### `getShapeMaxY()`

Vrací horní výšku extrudovaného tvaru.

### `getHoles()`

Vrací kolekci děr v podstavě (které se také extrudují).

### `centerPosition()`

Centruje pozici markeru podle aktuálního tvaru a výšek.

### `isDepthTestEnabled()` / `setDepthTestEnabled(boolean enabled)`

Nastavení viditelnosti přes překážky (depth-test).

### `getLineWidth()` / `setLineWidth(int width)`

Šířka obrysových čar.

### `getLineColor()` / `setLineColor(Color color)`

Barva obrysových čar.

### `getFillColor()` / `setFillColor(Color color)`

Barva výplně stěn tělesa.

### `setColors(Color lineColor, Color fillColor)`

Nastavení obou barev najednou.

### `builder()`

Vrací `Builder`.

## Vnořená třída `Builder`

Umožňuje plynulé vytváření `ExtrudeMarker`.

### Metody Builderu

- `shape(Shape shape, float minY, float maxY)`: Nastaví tvar a rozsah výšek.
- `holes(Shape... holes)`: Přidá díry.
- `clearHoles()`: Smaže díry.
- `centerPosition()`: Vycentruje.
- `depthTestEnabled(boolean enabled)`: Depth test.
- `lineWidth(int width)`: Šířka čar.
- `lineColor(Color color)`: Barva čar.
- `fillColor(Color color)`: Barva výplně.
- `build()`: Vytvoří instanci.
