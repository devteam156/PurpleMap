# TileModelView.java

## Přehled

`TileModelView` je wrapper (pohled) nad `TileModel`. Umožňuje pracovat pouze s určitou částí modelu (range), jako by to
byl samostatný model.

## Umístění

`de.bluecolored.bluemap.core.map.hires.TileModelView`

## Použití

Používá se v `RenderPass`ech. Každý render pass nebo renderer bloku dostane tento view, přidá do něj geometrii (voláním
`add`), a pak na tento view aplikuje transformace. Tyto transformace se provedou pouze na nově přidané geometrii (v
rozsahu definovaném view), aniž by ovlivnily zbytek podkladového modelu.

## Metody

- `initialize(TileModel model, ...)`: Nastaví podkladový model a počáteční offset.
- `add(int count)`: Deleguje na podkladový model a aktualizuje velikost view.
- Transformační metody (`rotate`, `scale`, `transform`...): Aplikují transformaci na podkladový model, ale pouze v
  rozsahu `[start, start + size]`.
- `reset()`: Vrátí velikost view na 0 (zahodí změny v rámci view, resetuje offset v modelu).
