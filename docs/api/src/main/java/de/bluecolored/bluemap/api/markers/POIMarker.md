# POIMarker.java

## Přehled

`POIMarker` (Point of Interest Marker) slouží k vyznačení bodu zájmu na mapě pomocí ikony (obrázku). Implementuje
rozhraní `DetailMarker` a `ElementMarker`.

## Umístění

`de.bluecolored.bluemap.api.markers.POIMarker`

## Dědičnost

`DistanceRangedMarker` -> `POIMarker`

## Konstruktory

### `POIMarker(String label, Vector3d position)`

Vytvoří POI marker s výchozí ikonou na zadané pozici.

### `POIMarker(String label, Vector3d position, String iconAddress, Vector2i anchor)`

Vytvoří POI marker s vlastní ikonou.

- `iconAddress`: Adresa (URL nebo cesta) k obrázku ikony.
- `anchor`: Bod ukotvení ikony (v pixelech vzhledem k obrázku), který bude odpovídat zadané `position`.

## Metody

### `getDetail()` / `setDetail(String detail)`

Získá nebo nastaví detailní popis, který se zobrazí po kliknutí na marker (nebo v seznamu).

### `getIconAddress()`

Vrací adresu aktuálně nastavené ikony.

### `getAnchor()` / `setAnchor(Vector2i anchor)`

Získá nebo nastaví bod ukotvení ikony.

### `setIcon(String iconAddress, int anchorX, int anchorY)`

Nastaví ikonu a její ukotvení pomocí souřadnic X a Y.

### `setIcon(String iconAddress, Vector2i anchor)`

Nastaví ikonu a její ukotvení pomocí vektoru.

### `getStyleClasses()` / `setStyleClasses(...)` / `addStyleClasses(...)`

Metody pro práci s CSS třídami, které lze aplikovat na HTML element markeru ve webové aplikaci.

### `builder()`

Vrací `Builder` pro vytváření instancí `POIMarker`.

## Vnořená třída `Builder`

Umožňuje plynulé vytváření `POIMarker`.

### Metody Builderu

- `detail(String detail)`: Nastaví detailní popis.
- `icon(String iconAddress, int anchorX, int anchorY)`: Nastaví ikonu a ukotvení.
- `defaultIcon()`: Resetuje ikonu na výchozí.
- `styleClasses(String... styleClasses)`: Přidá CSS třídy.
- `build()`: Vytvoří instanci `POIMarker`. Vyžaduje `label` a `position`.
