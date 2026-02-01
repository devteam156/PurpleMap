# PalettedPermutationsSource.java

## Přehled

`PalettedPermutationsSource` je pokročilý typ zdroje, který generuje varianty textur přebarvením (paletizací). Používá
se např. pro kožené brnění nebo lektvary, ale v kontextu bloků např. pro různé druhy dřeva, které používají stejný vzor,
jen jiné barvy.

## Umístění

`de.bluecolored.bluemap.core.resources.pack.resourcepack.atlas.PalettedPermutationsSource`

## Dědičnost

`Source` -> `PalettedPermutationsSource`

## Atributy (z JSONu)

- `textures`: Seznam základních textur, které se mají přebarvovat.
- `palette_key`: Textura (obrázek) obsahující klíčové barvy, které se mají nahrazovat.
- `permutations`: Mapa permutací. Klíč je sufix (např. "oak"), hodnota je cesta k textuře s cílovými barvami.

## Metody

### `load(...)`

Načte pouze zdrojové textury a palety do poolu. Samotné generování probíhá až v `bake()`.

### `bake(...)`

Vygeneruje nové textury.

1. Načte `palette_key` (obrázek s původními barvami).
2. Pro každou permutaci načte cílovou paletu.
3. Vytvoří mapování barev (původní -> cílová).
4. Pro každou základní texturu v `textures`:
    - Vytvoří novou texturu s názvem `původní_název + separator + sufix`.
    - Projde každý pixel původní textury a nahradí jeho barvu podle mapování.
    - Uloží novou texturu do poolu.
