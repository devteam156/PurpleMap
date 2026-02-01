# LiquidModelRenderer.java

## Přehled

`LiquidModelRenderer` je specializovaný renderer pro tekutiny (vodu a lávu). Tekutiny v Minecraftu nemají statický model
v resource packu, jejich tvar (výška hladiny, směr toku) se počítá dynamicky podle okolí.

## Umístění

`de.bluecolored.bluemap.core.map.hires.block.LiquidModelRenderer`

## Implementovaná Rozhraní

`BlockRenderer`

## Funkcionalita

1. **Výpočet výšky rohů:** Pro každý ze 4 rohů bloku vypočítá výšku hladiny na základě sousedních bloků (
   `getLiquidCornerHeight`).
2. **Culling (ořezávání):** Nevykresluje stěny, které sousedí se stejnou tekutinou nebo pevným blokem.
3. **Textury:** Používá textury `still` (stojatá) a `flow` (tekoucí) definované v resource packu.
4. **Směr toku:** Vypočítá vektor toku a podle něj natočí texturu na horní stěně.
5. **Barva:** Aplikuje barvu biomu (např. barva vody v bažině).
6. **Geometrie:** Vytváří model dynamicky modifikací výšky vrcholů.

## Metody

### `render(...)`

Hlavní metoda. Inicializuje data a volá `build()`.

### `build()`

Sestaví geometrii bloku.

- Získá ID textur.
- Vypočítá barvu biomu.
- Pro každou stěnu (UP, DOWN, NORTH...) volá `createElementFace`, pokud je viditelná.

### `getLiquidCornerHeight(...)`

Počítá výšku hladiny v rohu bloku průměrováním hladin sousedních bloků.

### `getFlowingAngle()`

Vypočítá úhel natočení textury pro tekoucí vodu.
