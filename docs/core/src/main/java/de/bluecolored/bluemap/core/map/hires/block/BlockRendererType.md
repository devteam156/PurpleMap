# BlockRendererType.java

## Přehled

`BlockRendererType` je registr a identifikátor typů rendererů bloků. Umožňuje definovat různé strategie vykreslování pro
různé typy bloků.

## Umístění

`de.bluecolored.bluemap.core.map.hires.block.BlockRendererType`

## Implementovaná Rozhraní

`Keyed`, `BlockRendererFactory`

## Konstanty / Registry

- `DEFAULT`: Standardní renderer pro bloky definované v resource packu (`ResourceModelRenderer`).
- `LIQUID`: Speciální renderer pro tekutiny (voda, láva), které mají dynamickou výšku a tok (`LiquidModelRenderer`).
- `MISSING`: Renderer pro chybějící bloky (`MissingModelRenderer`).
- `REGISTRY`: Registr všech dostupných typů.

## Metody

### `isFallbackFor(BlockState blockState)`

Určuje, zda tento typ rendereru může sloužit jako záloha pro daný blok, pokud pro něj neexistuje resource v resource
packu.

- Výchozí implementace vrací `false`.
- To může být využito např. pro dynamicky generované bloky z modů.

### `create(...)`

Deleguje na vnitřní továrnu.
