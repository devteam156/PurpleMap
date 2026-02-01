# DirectorySource.java

## Přehled

`DirectorySource` je typ zdroje v atlasu, který načte všechny textury z určitého adresáře (a jeho podadresářů).

## Umístění

`de.bluecolored.bluemap.core.resources.pack.resourcepack.atlas.DirectorySource`

## Dědičnost

`Source` -> `DirectorySource`

## Atributy (z JSONu)

- `source`: Cesta k adresáři uvnitř `textures` (např. "block").
- `prefix`: Volitelný prefix, který se přidá k názvům načtených textur (např. "block/").

## Metody

### `load(...)`

Prohledá zadaný adresář (`assets/<namespace>/textures/<source>`) a načte všechny `.png` soubory jako textury. Názvy
textur jsou relativní k adresáři `textures`.
