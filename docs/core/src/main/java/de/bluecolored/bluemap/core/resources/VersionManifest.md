# VersionManifest.java

## Přehled

`VersionManifest` je třída zodpovědná za stahování a parsování oficiálního manifestu verzí Minecraftu ze serverů
Mojangu (`piston-meta.mojang.com`). Slouží k vyhledání URL adres pro stažení klienta a serveru pro konkrétní verzi
Minecraftu.

## Umístění

`de.bluecolored.bluemap.core.resources.VersionManifest`

## Konstanty

- `MANIFEST_URL`: URL adresa hlavního manifestu (`.../version_manifest.json`).

## Metody

### `getOrFetch()` / `fetch()`

Získá (z cache) nebo stáhne aktuální manifest verzí.

### `getVersion(String id)`

Vrátí objekt `Version` pro zadané ID verze (např. "1.20.4"). Pokud verze neexistuje, vyhodí výjimku.

### `getVersions()`

Vrátí seznam všech dostupných verzí seřazený od nejnovější.

## Vnořené třídy (Data Classes)

- `Version`: Základní informace o verzi (ID, typ, URL detailu, čas vydání).
- `VersionDetail`: Detailní informace o verzi (stahuje se z URL v `Version`). Obsahuje sekci `downloads`.
- `Downloads`: Odkazy na stažení klienta a serveru.
- `Download`: Konkrétní soubor ke stažení (URL, SHA1, velikost).
