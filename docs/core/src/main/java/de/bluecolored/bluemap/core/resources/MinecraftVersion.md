# MinecraftVersion.java

## Přehled

`MinecraftVersion` slouží k detekci a stahování správných verzí Minecraft klientů (jar souborů) pro získání vanilla
zdrojů.

## Umístění

`de.bluecolored.bluemap.core.resources.MinecraftVersion`

## Balíček

`de.bluecolored.bluemap.core.resources`

## Atributy

- `id`: ID verze (např. "1.20.1").
- `resourcePack`: Cesta k JARu s resource packem.
- `resourcePackVersion`: Verze formátu resource packu.
- `dataPack`: Cesta k JARu s data packem.
- `dataPackVersion`: Verze formátu data packu.

## Statické Metody

### `load(...)`

Hlavní metoda pro načtení/stažení verze.

1. Získá manifest verzí (`VersionManifest.getOrFetch()`).
2. Pokud není zadáno ID, použije nejnovější release.
3. Určí verzi pro resource pack (min. 1.13) a data pack (min. 1.19.4).
4. Pokud je povoleno stahování (`allowDownload`) a soubory chybí, stáhne je.
5. Načte `version.json` z JARů pro zjištění verzí formátů packů.
6. Vrátí instanci `MinecraftVersion`.

### `download(...)`

Stáhne klientský JAR z Mojang serverů, ověří SHA-1 hash a uloží ho.

### `loadVersionInfo(Path file)`

Otevře JAR soubor, najde `version.json` a deserializuje ho.