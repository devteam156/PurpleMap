# RenderPassFactory.java

## Přehled

`RenderPassFactory` je funkcionální rozhraní (továrna) pro vytváření instancí `RenderPass`.

## Umístění

`de.bluecolored.bluemap.core.map.hires.RenderPassFactory`

## Metody

### `create(ResourcePack resourcePack, TextureGallery textureGallery, RenderSettings renderSettings)`

Vytvoří nový `RenderPass`.

- `resourcePack`: Zdroj modelů a textur.
- `textureGallery`: Galerie textur (pro získání ID textur).
- `renderSettings`: Nastavení renderování (co se má/nemá renderovat).
