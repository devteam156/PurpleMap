# PackExtension.java

## Přehled

`PackExtension` je rozhraní pro rozšíření funkčnosti balíčků zdrojů. Umožňuje přidat vlastní logiku načítání nebo
zpracování (baking) zdrojů.

## Umístění

`de.bluecolored.bluemap.core.resources.pack.PackExtension`

## Metody

### `loadResources(Iterable<Path> roots)`

Volá se během fáze načítání zdrojů. Umožňuje rozšíření načíst vlastní soubory.

### `bake()`

Volá se po načtení všech zdrojů. Slouží k finalizaci dat (např. sestavení atlasů textur, validace modelů).
