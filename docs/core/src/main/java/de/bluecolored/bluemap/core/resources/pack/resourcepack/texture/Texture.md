# Texture.java

## Přehled

`Texture` reprezentuje načtenou texturu z resource packu.

## Umístění

`de.bluecolored.bluemap.core.resources.pack.resourcepack.texture.Texture`

## Implementovaná Rozhraní

`Keyed`

## Atributy

- `resourcePath`: Cesta k textuře (klíč).
- `color`: Průměrná barva textury (používá se pro mapy a vzdálené pohledy).
- `halfTransparent`: Zda textura obsahuje poloprůhledné pixely.
- `texture`: Base64 kódovaný řetězec obrázku (pro použití ve webové aplikaci / JSONu).
- `animation`: Metadata animace (pokud existují).
- `textureImage`: `SoftReference` na `BufferedImage` (pro použití v rendereru, drží se v paměti jen když je potřeba).

## Metody

### `from(...)`

Statická tovární metoda. Vypočítá průměrnou barvu, zkontroluje průhlednost a zakóduje obrázek do Base64.

### `getTextureImage()`

Vrátí `BufferedImage`. Pokud byl uvolněn z paměti (SoftReference), dekóduje ho znovu z Base64 řetězce.
