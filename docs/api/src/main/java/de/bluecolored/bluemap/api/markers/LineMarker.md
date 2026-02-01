# LineMarker.java

## Přehled

`LineMarker` zobrazuje lomenou čáru (cestu) v 3D prostoru na mapě. Čára je definována pomocí objektu `Line`. Lze
nastavit tloušťku a barvu čáry a také chování depth-testu.

## Umístění

`de.bluecolored.bluemap.api.markers.LineMarker`

## Dědičnost

`ObjectMarker` -> `LineMarker`

## Konstruktory

### `LineMarker(String label, Line line)`

Vytvoří nový `LineMarker`. Pozice markeru (pro štítek atd.) bude automaticky nastavena na střed bounding boxu čáry.

- `label`: Popisek.
- `line`: Objekt `Line` definující body čáry.

### `LineMarker(String label, Vector3d position, Line line)`

Vytvoří nový `LineMarker` s explicitní pozicí.

- `position`: Pozice markeru.

## Metody

### `getLine()` / `setLine(Line line)`

Získá nebo nastaví objekt `Line`, který tento marker zobrazuje.

### `centerPosition()`

Přepočítá a nastaví pozici markeru na střed bounding boxu aktuální čáry.

### `isDepthTestEnabled()` / `setDepthTestEnabled(boolean enabled)`

Určuje, zda je aktivní depth-test (zda je čára viditelná přes bloky).

### `getLineWidth()` / `setLineWidth(int width)`

Získá nebo nastaví šířku čáry v pixelech.

### `getLineColor()` / `setLineColor(Color color)`

Získá nebo nastaví barvu čáry.

### `builder()`

Vrací `Builder` pro vytváření instancí `LineMarker`.

## Vnořená třída `Builder`

Umožňuje plynulé vytváření `LineMarker`.

### Metody Builderu

- `line(Line line)`: Nastaví čáru.
- `centerPosition()`: Automaticky vypočítá střed.
- `depthTestEnabled(boolean enabled)`: Nastaví depth-test.
- `lineWidth(int width)`: Nastaví šířku.
- `lineColor(Color color)`: Nastaví barvu.
- `build()`: Vytvoří instanci `LineMarker`.
