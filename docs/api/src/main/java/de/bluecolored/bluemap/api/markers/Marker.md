# Marker.java

## Přehled

`Marker` je abstraktní základní třída pro všechny typy markerů, které lze zobrazit na webové mapě. Definuje společné
vlastnosti jako je typ, popisek (label), pozice, řazení a viditelnost.

## Umístění

`de.bluecolored.bluemap.api.markers.Marker`

## Známé implementace

- `HtmlMarker`
- `POIMarker`
- `ShapeMarker`
- `ExtrudeMarker`
- `LineMarker`

## Konstruktory

### `Marker(String type, String label, Vector3d position)`

Vytvoří nový marker. Tento konstruktor je chráněný a určený pro použití v podtřídách.

- `type`: Interní identifikátor typu markeru.
- `label`: Popisek markeru.
- `position`: Pozice markeru ve světě.

## Metody

### `getType()`

Vrací typ markeru (ID typu).

### `getLabel()`

Vrací aktuální popisek markeru.

### `setLabel(String label)`

Nastaví nový popisek markeru.
**Poznámka:** HTML tagy v popisku budou automaticky escapovány (nahrazeny entitami), aby se předešlo narušení vzhledu
nebo XSS útokům.

### `getPosition()`

Vrací aktuální pozici markeru jako `Vector3d`.

### `setPosition(Vector3d position)`

Nastaví novou pozici markeru.

### `setPosition(double x, double y, double z)`

Nastaví novou pozici markeru pomocí souřadnic.

### `getSorting()`

Vrací hodnotu řazení (sorting). Menší čísla jsou řazena dříve v seznamech a menu. Výchozí hodnota je 0.

### `setSorting(int sorting)`

Nastaví hodnotu řazení.

### `isListed()`

Vrací `true`, pokud se marker zobrazuje v seznamu markerů na webu.

### `setListed(boolean listed)`

Určuje, zda se má marker zobrazovat v seznamu markerů (menu) na webu. I když je `false`, marker se stále zobrazuje na
mapě, ale není viditelný v postranním panelu.

### `equals(Object o)`

Porovnává marker s jiným objektem.

### `hashCode()`

Vrací hash kód markeru.

## Vnořená třída `Builder`

Abstraktní builder pro usnadnění vytváření instancí markerů v podtřídách.

### Společné metody Builderu

- `label(String label)`: Nastaví popisek.
- `position(Vector3d position)`: Nastaví pozici.
- `position(double x, double y, double z)`: Nastaví pozici.
- `sorting(Integer sorting)`: Nastaví řazení.
- `listed(Boolean listed)`: Nastaví zobrazení v seznamu.
