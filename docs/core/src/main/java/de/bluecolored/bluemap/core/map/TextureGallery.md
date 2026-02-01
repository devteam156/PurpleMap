# TextureGallery.java

## Přehled

`TextureGallery` spravuje mapování mezi texturami z resource packu (identifikovanými `ResourcePath<Texture>`) a
číselnými ID, které se používají v modelu dlaždice (`ArrayTileModel`). Toto mapování je nezbytné, protože model ukládá
textury jako indexy do pole, aby se šetřilo místo.

## Umístění

`de.bluecolored.bluemap.core.map.TextureGallery`

## Funkcionalita

- Udržuje mapu `ResourcePath -> TextureMapping`.
- Každá textura dostane přidělené unikátní ID (int).
- Umožňuje uložit (`writeTexturesFile`) a načíst (`readTexturesFile`) toto mapování do/z souboru `textures.json`.
- Třídí textury tak, aby průhledné textury byly zpracovány specifickým způsobem (pokud je to potřeba pro renderování).

## Metody

### `put(ResourcePath<Texture> textureResourcePath)`

Zaregistruje texturu do galerie. Pokud již existuje, aktualizuje odkaz na objekt textury (např. po reloadu resource
packu), ale zachová původní ID.

### `get(ResourcePath<Texture> textureResourcePath)`

Vrátí číselné ID pro danou texturu.

### `writeTexturesFile(OutputStream out)`

Uloží seznam textur (seřazený podle ID) do JSON souboru.

### `readTexturesFile(InputStream in)`

Načte mapování textur ze souboru. Používá se při načítání existující mapy, aby se zajistila konzistence ID textur s již
vyrenderovanými dlaždicemi.
