# Variants.java

## Přehled

`Variants` reprezentuje sekci `variants` v souboru blockstate. Obsahuje mapování mezi stavy bloku (podmínkami) a sadami
variant (`VariantSet`).

## Umístění

`de.bluecolored.bluemap.core.resources.pack.resourcepack.blockstate.Variants`

## Atributy

- `variants`: Pole sad variant, kde každá sada má přiřazenou podmínku.
- `defaultVariant`: Výchozí sada variant (pro případ, že podmínka je "normal" nebo "default").

## Metody

### `forEach(BlockState blockState, int x, int y, int z, Consumer<Variant> consumer)`

Najde první `VariantSet`, jehož podmínka odpovídá danému `BlockState`.

- Poté v nalezené sadě vybere konkrétní variantu (náhodně podle pozice x, y, z a vah) a předá ji consumerovi.
- Pokud žádná podmínka nesedí, použije `defaultVariant`.

## Vnořená třída `Adapter`

GSON adaptér, který parsuje mapu `{"key=value": { ... }}` na seznam objektů s podmínkami.
