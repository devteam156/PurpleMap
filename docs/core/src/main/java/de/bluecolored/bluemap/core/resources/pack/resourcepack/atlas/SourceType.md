# SourceType.java

## Přehled

`SourceType` je registr typů zdrojů v atlasu. Mapuje textový identifikátor typu (např. `single`) na třídu implementující
`Source`.

## Umístění

`de.bluecolored.bluemap.core.resources.pack.resourcepack.atlas.SourceType`

## Implementovaná Rozhraní

`Keyed`

## Konstanty / Registry

- `single`: `SingleSource`
- `directory`: `DirectorySource`
- `filter`: `Source` (jen filtruje, nenačítá nic nového)
- `unstitch`: `UnstitchSource`
- `paletted_permutations`: `PalettedPermutationsSource`

## Metody

- `getType()`: Vrací třídu odpovídající tomuto typu zdroje.
