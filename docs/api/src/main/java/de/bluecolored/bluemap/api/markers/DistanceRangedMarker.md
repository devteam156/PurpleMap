# DistanceRangedMarker.java

## Přehled

`DistanceRangedMarker` je abstraktní třída, která rozšiřuje základní `Marker`. Přidává funkcionalitu pro řízení
viditelnosti markeru na základě vzdálenosti kamery. To umožňuje skrývat markery, které jsou příliš blízko nebo příliš
daleko od pozorovatele.

## Umístění

`de.bluecolored.bluemap.api.markers.DistanceRangedMarker`

## Dědičnost

`Marker` -> `DistanceRangedMarker`

## Známé implementace

- `HtmlMarker`
- `POIMarker`
- `ShapeMarker`
- `ExtrudeMarker`
- `LineMarker`
- `ObjectMarker`

## Konstruktory

### `DistanceRangedMarker(String type, String label, Vector3d position)`

Vytvoří nový `DistanceRangedMarker` s výchozími hodnotami vzdálenosti:

- `minDistance`: 0.0 (vždy viditelný zblízka)
- `maxDistance`: 10 000 000.0 (viditelný z velké dálky)

## Metody

### `getMinDistance()`

Vrací minimální vzdálenost kamery od markeru, při které je marker ještě viditelný. Pokud je kamera blíže než tato
hodnota, marker se skryje.

### `setMinDistance(double minDistance)`

Nastaví minimální vzdálenost pro zobrazení markeru.

### `getMaxDistance()`

Vrací maximální vzdálenost kamery od markeru, při které je marker ještě viditelný. Pokud je kamera dále než tato
hodnota, marker se skryje.

### `setMaxDistance(double maxDistance)`

Nastaví maximální vzdálenost pro zobrazení markeru.

### `equals(Object o)`

Porovnává marker s jiným objektem (včetně porovnání `minDistance` a `maxDistance`).

### `hashCode()`

Vrací hash kód markeru.

## Vnořená třída `Builder`

Abstraktní builder rozšiřující `Marker.Builder`, přidávající metody pro nastavení vzdáleností.

### Metody Builderu

- `minDistance(double minDistance)`: Nastaví minimální vzdálenost.
- `maxDistance(double maxDistance)`: Nastaví maximální vzdálenost.
