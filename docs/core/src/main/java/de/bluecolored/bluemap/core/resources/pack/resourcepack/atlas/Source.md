# Source.java

## Přehled

`Source` je abstraktní základní třída pro zdroje v atlasu. Obsahuje společnou logiku pro načítání textur a jejich
metadat (animací).

## Umístění

`de.bluecolored.bluemap.core.resources.pack.resourcepack.atlas.Source`

## Atributy (z JSONu)

- `type`: Typ zdroje (např. `directory`, `single`, `paletted_permutations`).

## Metody

### `load(...)` / `bake(...)`

Metody pro načítání a zpracování zdrojů (implementují podtřídy).

### `loadTexture(...)`

Načte texturu ze souboru.

- Načte obrázek (`loadImage`).
- Načte metadata animace (`loadAnimation`) ze souboru `.png.mcmeta`.
- Vytvoří objekt `Texture`.

### `loadImage(Path imageFile)`

Načte `BufferedImage` ze souboru.

### `loadAnimation(Path imageFile)`

Načte `AnimationMeta` ze souboru `.png.mcmeta`.

### `getFile(...)`

Převede `ResourcePath` na fyzickou cestu k souboru v resource packu.

## Vnořená třída `Adapter`

GSON adaptér, který na základě pole `type` v JSONu rozhodne, jakou podtřídu `Source` instanciovat (polymorfní
deserializace).
