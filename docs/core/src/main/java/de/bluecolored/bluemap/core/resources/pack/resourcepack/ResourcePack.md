# ResourcePack.java

## Přehled

`ResourcePack` je třída, která spravuje načítání a přístup ke zdrojům Minecraftu (textury, modely, blokové stavy).
Vychází z třídy `Pack`.

## Umístění

`de.bluecolored.bluemap.core.resources.pack.resourcepack.ResourcePack`

## Balíček

`de.bluecolored.bluemap.core.resources.pack.resourcepack`

## Dědičnost

`Pack` -> `ResourcePack`

## Atributy

### `MISSING_...`

- **Typ:** `ResourcePath`
- **Popis:** Konstanty definující cesty k "missing" (chybějícím) zdrojům pro bloky, entity, modely a textury.

### `BLOCKS_ATLAS`

- **Typ:** `Key`
- **Popis:** Klíč pro atlas bloků (`minecraft:blocks`).

### Resource Pooly

- `atlases`: `ResourcePool<Atlas>`
- `blockStates`: `ResourcePool<BlockState>`
- `entityStates`: `ResourcePool<EntityState>`
- `models`: `ResourcePool<Model>`
- `textures`: `ResourcePool<Texture>`
- `colormaps`: `ResourcePool<BufferedImage>` (pro barvy listí, trávy atd.)

### `colorCalculatorFactory`

- **Typ:** `BlockColorCalculatorFactory`
- **Popis:** Továrna pro kalkulátory barev bloků. Načítá se z `blockColors.json`.

### `blockPropertiesConfig`

- **Typ:** `BlockPropertiesConfig`
- **Popis:** Konfigurace vlastností bloků (culling, okluze...). Načítá se z `blockProperties.json`.

### Cache

- `blockStateCache`: Cache pro mapování herních `BlockState` (z jádra) na resource `BlockState`.
- `blockPropertiesCache`: Cache pro vlastnosti bloků.

### `extensions`

- **Typ:** `Map<Extension<?>, ResourcePackExtension>`
- **Popis:** Rozšíření resource packu (např. pro podporu modů).

## Konstruktory

### `ResourcePack(PackVersion packVersion)`

Inicializuje prázdné pooly, továrny a cache. Aktivuje všechna registrovaná rozšíření.

## Metody

### `loadResources(Iterable<Path> roots)`

Hlavní metoda pro načtení zdrojů.

1. Projiteruje všechny kořenové adresáře (`roots`) a načte základní zdroje (jsony, textury).
2. Načte zdroje pro rozšíření.
3. Sesbírá klíče všech použitých textur (aby se nenačítaly nepotřebné textury).
4. Načte samotné textury do atlasu.
5. Provede "bake" (zapečení) - finalizaci zdrojů.

### `bake(Predicate<Key> textureFilter)`

1. Zapeče textury do atlasu.
2. Optimalizuje reference v modelech.
3. Aplikuje rodičovské modely (dědičnost modelů).
4. Vypočítá vlastnosti modelů.
5. Nastaví colormapy (foliage, grass...) do `colorCalculatorFactory`.

### `loadResources(Path root)` (privátní)

Načítá konkrétní typy souborů z daného kořene paralelně (pomocí `CompletableFuture`):

- Atlasy (`assets/*/atlases/*.json`)
- BlockStates (`assets/*/blockstates/*.json`)
- EntityStates (`assets/*/entitystates/*.json`)
- Modely (`assets/*/models/*.json`)
- Colormapy (`assets/minecraft/textures/colormap/*.png`)
- Konfigurace barev (`assets/*/blockColors.json`)
- Konfigurace vlastností (`assets/*/blockProperties.json`)

### `getBlockState(BlockState blockState)`

Vrátí resource `BlockState` odpovídající hernímu `BlockState`.

### `getBlockProperties(BlockState state)`

Vrátí vlastnosti bloku (průhlednost, culling...) pro daný stav. Zohledňuje konfiguraci, rozšíření a model bloku.