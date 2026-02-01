# Pack.java

## Přehled

`Pack` je abstraktní základní třída pro reprezentaci balíčku zdrojů (Resource Pack nebo Data Pack). Zajišťuje načítání
zdrojů ze souborového systému (adresáře nebo ZIP/JAR soubory).

## Umístění

`de.bluecolored.bluemap.core.resources.pack.Pack`

## Atributy

- `packVersion`: Verze formátu balíčku (např. 4 pro 1.13, 15 pro 1.20).
- `enabledFeatures`: Volitelná množina povolených funkcí (features) z `pack.mcmeta`. Pokud balíček vyžaduje funkci,
  která není povolena, nebude načten.

## Metody

### `loadResources(Iterable<Path> roots)`

Abstraktní metoda pro načtení zdrojů. Implementují ji konkrétní třídy jako `ResourcePack` nebo `DataPack`.

### `loadResourcePath(Path root, Loader resourceLoader)`

Rekurzivně prochází a načítá zdroje z daného kořenového adresáře.

- Podporuje vnořené JAR soubory (např. `fabric.mod.json` -> `jars`).
- Čte `pack.mcmeta` pro kontrolu kompatibility a funkcí.
- Podporuje vnořené datapacky (ve složce `data/datapacks`).
- Podporuje "overlays" (překryvné vrstvy pro různé verze formátu) definované v `pack.mcmeta`.
- Nakonec zavolá `resourceLoader.load(root)` pro načtení vlastních souborů v daném adresáři.
