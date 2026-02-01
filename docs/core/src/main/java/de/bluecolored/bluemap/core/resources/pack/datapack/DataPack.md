# DataPack.java

## Přehled

`DataPack` spravuje data world-genu (dimenze, biomy). Vychází z třídy `Pack`.

## Umístění

`de.bluecolored.bluemap.core.resources.pack.datapack.DataPack`

## Balíček

`de.bluecolored.bluemap.core.resources.pack.datapack`

## Dědičnost

`Pack` -> `DataPack`

## Konstanty

Definuje klíče pro standardní dimenze (`overworld`, `the_nether`, `the_end`).

## Atributy

- `dimensionTypes`: `ResourcePool<DimensionType>` - definice typů dimenzí (výška světa, light level atd.).
- `biomes`: `ResourcePool<Biome>` - definice biomů (barvy vody, trávy...).
- `legacyBiomes`: `LegacyBiomes` - podpora pro starší verze MC.

## Metody

### `loadResources(Iterable<Path> roots)`

Načte data ze všech kořenových adresářů a provede bake.

### `loadPath(Path root)` (privátní)

Načítá:

- Typy dimenzí z `data/*/dimension_type/*.json`.
- Biomy z `data/*/worldgen/biome/*.json`.

### `bake()`

Přidá výchozí (hardcoded) typy dimenzí, pokud chybí, a inicializuje `legacyBiomes`.

### `getDimensionType(Key key)`

Vrátí typ dimenze podle klíče.

### `getBiome(Key key)`

Vrátí biom podle klíče.