# HtmlMarker.java

## Přehled

`HtmlMarker` umožňuje umístit libovolný HTML prvek na mapu na konkrétní souřadnice. Tento marker se chová jako 2D
prvek "přilepený" k obrazovce, ale jeho pozice sleduje 3D souřadnice ve světě.

## Umístění

`de.bluecolored.bluemap.api.markers.HtmlMarker`

## Dědičnost

`DistanceRangedMarker` -> `HtmlMarker`

## Implementovaná Rozhraní

- `ElementMarker`

## Konstruktory

### `HtmlMarker(String label, Vector3d position, String html)`

Vytvoří nový HTML marker. Kotva (anchor) je ve výchozím nastavení (0, 0).

- `label`: Popisek markeru.
- `position`: Pozice ve světě.
- `html`: HTML kód, který se má zobrazit.

### `HtmlMarker(String label, Vector3d position, String html, Vector2i anchor)`

Vytvoří nový HTML marker s definovanou kotvou.

- `anchor`: Bod v pixelech (relativně k levému hornímu rohu HTML prvku), který bude sedět přesně na `position`.

## Metody

### `getHtml()`

Vrací HTML kód markeru.

### `setHtml(String html)`

Nastaví HTML kód markeru.
**Důležité:** Je nutné ošetřit uživatelské vstupy v HTML, aby se předešlo XSS útokům.

### `getAnchor()` / `setAnchor(Vector2i anchor)`

Získá nebo nastaví bod ukotvení (v pixelech).

### `getStyleClasses()` / `setStyleClasses(...)` / `addStyleClasses(...)`

Metody pro správu CSS tříd elementu.

### `builder()`

Vrací `Builder` pro vytváření instancí `HtmlMarker`.

## Vnořená třída `Builder`

Umožňuje plynulé vytváření `HtmlMarker`.

### Metody Builderu

- `html(String html)`: Nastaví HTML obsah.
- `anchor(Vector2i anchor)`: Nastaví kotvu.
- `anchor(int x, int y)`: Nastaví kotvu.
- `styleClasses(...)`: Nastaví CSS třídy.
- `build()`: Vytvoří instanci `HtmlMarker`.
