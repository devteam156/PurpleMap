# Multipart.java

## Přehled

`Multipart` reprezentuje sekci `multipart` v souboru blockstate. Umožňuje skládat model bloku z více nezávislých částí
na základě podmínek.

## Umístění

`de.bluecolored.bluemap.core.resources.pack.resourcepack.blockstate.Multipart`

## Atributy

- `parts`: Seznam částí (`VariantSet`), kde každá část má podmínku (`when`) a aplikované modely (`apply`).

## Metody

### `forEach(BlockState blockState, ...)`

Projde všechny části. Pokud část splňuje podmínku (`condition.matches(blockState)`), aplikuje její varianty (zavolá
`consumer`).

## Vnořená třída `Adapter`

GSON adaptér pro načítání multipart definice. Zvládá rekurzivní parsování podmínek (AND, OR).
