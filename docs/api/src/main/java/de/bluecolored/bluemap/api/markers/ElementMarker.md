# ElementMarker.java

## Přehled

`ElementMarker` je rozhraní, které definuje společné vlastnosti pro markery, které jsou ve webové aplikaci
reprezentovány jako HTML elementy (např. `POIMarker`, `HtmlMarker`).

## Umístění

`de.bluecolored.bluemap.api.markers.ElementMarker`

## Známé implementace

- `HtmlMarker`
- `POIMarker`

## Konstanty

- `STYLE_CLASS_PATTERN`: Regulární výraz (`-?[_a-zA-Z]+[_a-zA-Z0-9-]*`), který definuje povolený formát CSS tříd.

## Metody

### `getAnchor()`

Vrací bod ukotvení (`Vector2i` v pixelech), který určuje, jak je element posunut vzhledem k jeho logické pozici na mapě.

### `setAnchor(Vector2i anchor)`

Nastaví bod ukotvení.

### `setAnchor(int x, int y)`

Nastaví bod ukotvení pomocí souřadnic X a Y.

### `getStyleClasses()`

Vrací neměnnou kolekci řetězců představujících CSS třídy přiřazené tomuto elementu.

### `setStyleClasses(Collection<String> styleClasses)`

Nastaví CSS třídy. Nahradí všechny existující třídy.

- Vyhodí `IllegalArgumentException`, pokud některá třída neodpovídá `STYLE_CLASS_PATTERN`.

### `setStyleClasses(String... styleClasses)`

Varargs verze pro `setStyleClasses`.

### `addStyleClasses(Collection<String> styleClasses)`

Přidá nové CSS třídy k existujícím.

- Vyhodí `IllegalArgumentException`, pokud formát nesedí.

### `addStyleClasses(String... styleClasses)`

Varargs verze pro `addStyleClasses`.

## Vnořené rozhraní `Builder`

Rozhraní pro buildery tříd, které implementují `ElementMarker`.

### Metody Builderu

- `anchor(Vector2i anchor)`: Nastaví kotvu.
- `anchor(int x, int y)`: Nastaví kotvu.
- `styleClasses(String... styleClasses)`: Přidá CSS třídy.
- `clearStyleClasses()`: Odstraní všechny CSS třídy.
