# MissingModelRenderer.java

## Přehled

`MissingModelRenderer` je záložní renderer, který se používá, když pro daný blok není nalezen žádný jiný vhodný
renderer (např. chybí model v resource packu).

## Umístění

`de.bluecolored.bluemap.core.map.hires.block.MissingModelRenderer`

## Implementovaná Rozhraní

`BlockRenderer`

## Funkcionalita

- Používá cache `BLOCK_RENDERER_TYPES` k nalezení fallback rendereru pro daný `BlockState`.
- Pokud fallback existuje (např. definovaný jiným rendererem jako `isFallbackFor`), použije ho.
- Pokud fallback neexistuje, použije `BlockRendererType.DEFAULT` (což obvykle vede k vykreslení fialovo-černé kostky "
  missing texture/model" definované v BlueMap resource packu).

## Metody

### `render(...)`

Deleguje renderování na nalezený nebo výchozí renderer.
