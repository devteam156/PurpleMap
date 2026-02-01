# BlockRenderer.java

## Přehled

`BlockRenderer` je rozhraní pro komponentu, která dokáže vykreslit jeden konkrétní blok (jeho variantu) do modelu.

## Umístění

`de.bluecolored.bluemap.core.map.hires.block.BlockRenderer`

## Metody

### `render(BlockNeighborhood block, Variant variant, TileModelView tileModel, Color blockColor)`

Vykreslí blok.

- `block`: Informace o bloku a jeho sousedech (pro kontext, např. napojování plotů).
- `variant`: Konkrétní varianta block-state (model, textury) z resource packu.
- `tileModel`: Pohled na model, do kterého se má geometrie bloku přidat.
- `blockColor`: Výstupní parametr (objekt `Color`), do kterého renderer zapíše průměrnou barvu bloku (pro low-res mapu).

**Poznámka k vláknům:** Implementace zaručuje, že tato metoda je volána pouze jedním vláknem pro danou instanci
rendereru.
