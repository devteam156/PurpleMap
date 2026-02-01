# AnimationMeta.java

## Přehled

`AnimationMeta` obsahuje metadata o animaci textury, načtená ze souboru `.png.mcmeta`.

## Umístění

`de.bluecolored.bluemap.core.resources.pack.resourcepack.texture.AnimationMeta`

## Atributy (z JSONu)

- `interpolate`: Zda se má interpolovat mezi snímky.
- `width`, `height`: Rozměry jednoho snímku (pokud se liší od standardních).
- `frametime`: Výchozí doba trvání snímku.
- `frames`: Seznam snímků (`FrameMeta`).

## Vnořená třída `FrameMeta`

Definuje index snímku a volitelně jeho specifickou dobu trvání.
