# DetailMarker.java

## Přehled

`DetailMarker` je rozhraní, které definuje metody pro markery, které mohou mít detailní popis (popup).

## Umístění

`de.bluecolored.bluemap.api.markers.DetailMarker`

## Známé implementace

- `POIMarker`
- `ObjectMarker` (a jeho potomci: `ShapeMarker`, `ExtrudeMarker`, `LineMarker`)

## Metody

### `getDetail()`

Vrací text detailu markeru. Tento text může obsahovat HTML tagy.

### `setDetail(String detail)`

Nastaví detailní text markeru.
**Důležité:** HTML tagy v tomto textu **nejsou escapovány**. To umožňuje formátování textu, ale vyžaduje opatrnost při
vkládání uživatelských vstupů, aby se předešlo XSS útokům.

## Vnořené rozhraní `Builder`

Rozhraní pro buildery tříd, které implementují `DetailMarker`.

### Metody Builderu

- `detail(String detail)`: Nastaví detail markeru.
