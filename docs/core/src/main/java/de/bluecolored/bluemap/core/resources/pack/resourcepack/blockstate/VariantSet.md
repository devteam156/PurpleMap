# VariantSet.java

## Přehled

`VariantSet` je skupina variant, které platí pro stejnou podmínku (stav bloku). Pokud obsahuje více variant, jedna se
vybere náhodně (váženým výběrem).

## Umístění

`de.bluecolored.bluemap.core.resources.pack.resourcepack.blockstate.VariantSet`

## Atributy

- `condition`: Podmínka, kdy tato sada platí.
- `variants`: Pole možných variant.
- `totalWeight`: Součet vah všech variant.

## Metody

### `forEach(int x, int y, int z, Consumer<Variant> consumer)`

Vybere jednu variantu ze sady na základě pozice bloku (`hashToFloat`) a vah variant. Tím se zajistí, že stejný blok na
stejném místě bude mít vždy stejný vzhled (deterministický "náhodný" výběr).

### `hashToFloat(...)`

Generuje pseudonáhodné číslo 0.0 - 1.0 na základě souřadnic.
