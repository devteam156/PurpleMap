# ObjectMarker.java

## Přehled

`ObjectMarker` je abstraktní základní třída pro markery, které reprezentují nějaký objekt nebo tvar na mapě (např.
`ShapeMarker`, `LineMarker`, `ExtrudeMarker`). Poskytuje společnou funkcionalitu pro popisky, detaily a odkazy.

## Umístění

`de.bluecolored.bluemap.api.markers.ObjectMarker`

## Dědičnost

`DistanceRangedMarker` -> `ObjectMarker`

## Implementovaná Rozhraní

- `DetailMarker`: Marker může mít detailní popis.

## Konstruktory

### `ObjectMarker(String type, String label, Vector3d position)`

Konstruktor pro podtřídy.

- `type`: Typ markeru (pro interní použití v BlueMap).
- `label`: Popisek markeru.
- `position`: Pozice markeru.

## Metody

### `getDetail()` / `setDetail(String detail)`

Získá nebo nastaví detailní text markeru. Ve výchozím nastavení je detail shodný s `label`, pokud není nastaven jinak.

### `getLink()`

Vrací `Optional<String>` obsahující URL odkazu, pokud je nastaven.

### `isNewTab()`

Vrací `true`, pokud se má odkaz otevírat v nové záložce prohlížeče.

### `setLink(String link, boolean newTab)`

Nastaví odkaz, který se otevře po kliknutí na marker.

- `link`: URL adresa.
- `newTab`: Zda otevřít v novém okně/záložce.

### `removeLink()`

Odstraní odkaz z markeru.

### `builder()`

Statická metoda `builder()` není přímo v této třídě (třída je abstraktní), ale podtřídy mají své buildery, které dědí z
`ObjectMarker.Builder`.

## Vnořená třída `Builder`

Abstraktní builder, který poskytuje metody pro nastavení společných vlastností `ObjectMarker`.

### Společné metody Builderu

- `detail(String detail)`: Nastaví detail.
- `link(String link, boolean newTab)`: Nastaví odkaz.
- `noLink()`: Odstraní odkaz.
