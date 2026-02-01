# Atlas.java

## Přehled

`Atlas` reprezentuje sadu zdrojů textur, které se používají v resource packu. Odpovídá souborům v
`assets/<namespace>/atlases/*.json`.

## Umístění

`de.bluecolored.bluemap.core.resources.pack.resourcepack.atlas.Atlas`

## Atributy

- `sources`: Seznam zdrojů (`Source`), které definují, jak a odkud se mají textury načíst.

## Metody

### `add(Atlas atlas)`

Přidá zdroje z jiného atlasu do tohoto atlasu.

### `load(Path root, ResourcePool<Texture> textures, Predicate<Key> textureFilter)`

Spustí načítání textur ze všech zdrojů.

- `root`: Kořenový adresář resource packu.
- `textures`: Pool, do kterého se mají textury uložit.
- `textureFilter`: Filtr, který určuje, které textury se mají načíst (optimalizace).

### `bake(ResourcePool<Texture> textures, Predicate<Key> textureFilter)`

Spustí "pečení" (baking) pro všechny zdroje. Některé zdroje (např. `PalettedPermutationsSource`) generují textury až v
této fázi, protože potřebují mít již načtené jiné textury (palety).
