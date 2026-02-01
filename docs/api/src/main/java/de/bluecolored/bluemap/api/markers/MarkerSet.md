# MarkerSet.java

## Přehled

`MarkerSet` je kontejner (sada) pro `Marker`y. Ve webové aplikaci BlueMap jsou markery organizovány právě do těchto sad.
Každá sada může mít svůj název, může být skryvatelná (toggleable) a může být ve výchozím stavu skrytá.

## Umístění

`de.bluecolored.bluemap.api.markers.MarkerSet`

## Konstruktory

### `MarkerSet(String label)`

Vytvoří novou sadu markerů s daným názvem. Ve výchozím nastavení je přepínatelná (`toggleable = true`) a viditelná (
`defaultHidden = false`).

### `MarkerSet(String label, boolean toggleable, boolean defaultHidden)`

Vytvoří novou sadu s plnou konfigurací.

## Metody

### `getLabel()` / `setLabel(String label)`

Získá nebo nastaví název sady. Tento název se zobrazuje v menu mapy.

### `isToggleable()` / `setToggleable(boolean toggleable)`

Určuje, zda uživatel může tuto sadu v prohlížeči zapínat a vypínat (zda má přepínač).

### `isDefaultHidden()` / `setDefaultHidden(boolean defaultHidden)`

Určuje, zda je sada markerů po načtení stránky ve výchozím stavu skrytá.

### `getSorting()` / `setSorting(int sorting)`

Získá nebo nastaví pořadí řazení této sady v menu. Nižší číslo znamená dřívější pozici (např. 0 je před 1).

### `getMarkers()`

Vrací `Map<String, Marker>`, která obsahuje všechny markery v této sadě. Klíčem je ID markeru.

- Mapa je `ConcurrentHashMap`, takže je bezpečná pro vlákna.
- Do této mapy lze přímo přidávat nebo odebírat markery.

### `get(String key)`

Zkratka pro `getMarkers().get(key)`. Získá marker podle ID.

### `put(String key, Marker marker)`

Zkratka pro `getMarkers().put(key, marker)`. Přidá marker do sady pod daným ID.

### `remove(String key)`

Zkratka pro `getMarkers().remove(key)`. Odstraní marker ze sady.

### `builder()`

Vrací `Builder` pro vytváření instancí `MarkerSet`.

## Vnořená třída `Builder`

Umožňuje plynulé vytváření `MarkerSet`.

### Metody Builderu

- `label(String label)`: Nastaví název.
- `toggleable(Boolean toggleable)`: Nastaví přepínatelnost.
- `defaultHidden(Boolean defaultHidden)`: Nastaví výchozí viditelnost.
- `sorting(Integer sorting)`: Nastaví pořadí.
- `build()`: Vytvoří instanci `MarkerSet`.
