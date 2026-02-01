# BlockRendererFactory.java

## Přehled

`BlockRendererFactory` je funkcionální rozhraní (továrna) pro vytváření instancí `BlockRenderer`.

## Umístění

`de.bluecolored.bluemap.core.map.hires.block.BlockRendererFactory`

## Metody

### `create(ResourcePack resourcePack, TextureGallery textureGallery, RenderSettings renderSettings)`

Vytvoří nový `BlockRenderer` (např. pro standardní bloky, tekutiny atd.).

- `resourcePack`: Zdroj modelů a textur.
- `textureGallery`: Galerie pro získání ID textur.
- `renderSettings`: Nastavení renderování.
