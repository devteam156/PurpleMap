# Model.java

## Přehled

`Model` reprezentuje celý 3D model bloku nebo entity načtený z resource packu (`models/**/*.json`).

## Umístění

`de.bluecolored.bluemap.core.resources.pack.resourcepack.model.Model`

## Atributy (z JSONu)

- `parent`: Odkaz na rodičovský model (dědičnost).
- `textures`: Mapa proměnných textur (např. `#all`, `#top`).
- `elements`: Seznam elementů modelu.
- `ambientocclusion`: Zda model používá ambient occlusion.

## Metody

### `applyParent(ResourcePool<Model> modelPool)`

Aplikuje dědičnost. Načte rodičovský model a zkopíruje z něj chybějící atributy (elementy, textury, nastavení AO) do
tohoto modelu.

### `calculateProperties(...)`

Vypočítá odvozené vlastnosti modelu, jako je `occluding` (zda blok blokuje světlo) a `culling` (zda blok skrývá sousední
stěny), na základě jeho geometrie a průhlednosti textur.

### `optimize(...)`

Optimalizuje odkazy na textury (nahradí textové odkazy přímými objekty z poolu).
