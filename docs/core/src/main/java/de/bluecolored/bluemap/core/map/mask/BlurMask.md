# BlurMask.java

## Přehled

`BlurMask` je implementace `Mask`, která vytváří efekt rozmazání (nebo spíše rozšíření/margin) kolem jiné masky. Používá
se k zajištění, že se vyrenderuje dostatečné okolí kolem požadované oblasti, aby nedocházelo k chybám na okrajích (např.
chybějící světlo nebo AO).

## Umístění

`de.bluecolored.bluemap.core.map.mask.BlurMask`

## Atributy

- `masks`: Původní maska (nebo kombinace masek), která se má "rozmazat".
- `size`: Velikost rozšíření (poloměr) v blocích.

## Metody

### `test(int x, int y, int z)`

Testuje, zda je bod uvnitř masky.

- Místo jednoduchého rozšíření používá pseudonáhodný offset (`randomOffset`) pro testování původní masky. To vytváří "
  rozmazaný" okraj s ditheringem.

### `test(minX, minY, minZ, maxX, maxY, maxZ)`

Testuje, zda oblast (AABB) koliduje s maskou.

- Zde se provádí skutečné rozšíření hranic testované oblasti o `size`.
