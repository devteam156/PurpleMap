# BlockStateModelRenderer.java

## Přehled

`BlockStateModelRenderer` je "hlavní" renderer pro bloky. Nerozhoduje přímo o geometrii, ale deleguje práci na konkrétní
`BlockRenderer` podle typu bloku (varianty).

## Umístění

`de.bluecolored.bluemap.core.map.hires.block.BlockStateModelRenderer`

## Funkcionalita

- Používá `ResourcePack` k nalezení definice bloku (`BlockStateResource`).
- Z definice získá varianty bloku pro danou pozici (např. náhodné rotace, multipart bloky jako ploty).
- Pro každou variantu zjistí její `BlockRendererType` (např. `DEFAULT` nebo `LIQUID`).
- Používá cache (`blockRenderers`) pro instanciování a znovupoužití konkrétních rendererů.
- Agreguje výsledky (barvu) z více variant do jedné výsledné barvy bloku.
- Řeší **waterlogging** (zatopené bloky): Pokud je blok zatopený, vykreslí navíc variantu vody přes blok.

## Metody

### `render(BlockNeighborhood block, TileModelView blockModel, Color blockColor)`

Vykreslí blok. Pokud je to vzduch, nedělá nic. Pokud je zatopený, vykreslí i vodu.
