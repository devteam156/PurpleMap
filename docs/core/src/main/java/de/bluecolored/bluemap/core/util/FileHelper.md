# FileHelper.java

## Přehled

`FileHelper` obsahuje pokročilé nástroje pro práci se soubory, které standardní Java NIO neposkytuje nebo které vyžadují
specifické ošetření pro stabilitu aplikace.

## Umístění

`de.bluecolored.bluemap.core.util.FileHelper`

## Klíčové Metody a Logika

### `createFilepartOutputStream(Path file)`

- **Účel:** Bezpečný zápis souborů.
- **Logika:**
    1. Vytvoří dočasný soubor s příponou `.filepart`.
    2. Vrátí stream zapisující do tohoto souboru.
    3. **OnClose:** Při uzavření streamu automaticky provede atomické přejmenování (`atomicMove`) na cílový soubor. Tím
       se zabrání vzniku poloprázdných nebo poškozených souborů při pádu aplikace během zápisu.

### `atomicMove(Path from, Path to)`

- **Logika:** Pokusí se o skutečně atomický přesun na úrovni OS (`ATOMIC_MOVE`). Pokud to OS nebo souborový systém
  nepodporuje (např. přesun mezi disky), provede standardní přesun s nahrazením.

### `extractZipFile(...)`

- **Logika:** Rozbalí ZIP archiv do cílové složky. Používá vlastní `FileSystem` pro ZIP, projde celý strom (
  `walkFileTree`) a kopíruje soubory pomocí `CopyingPathVisitor`.

### `awaitExistence(Path path, long timeout, TimeUnit unit)`

- **Logika:** Aktivně čeká, až se soubor nebo složka objeví na disku. Používá `WatchService` na rodičovském adresáři,
  takže neprovádí zbytečný "busy-waiting", ale reaguje na systémové události.

### `walk(Path start, ...)`

- **Účel:** Odolnější procházení souborového systému.
- **Logika:** Na rozdíl od `Files.walk` tato metoda ignoruje `NoSuchFileException`. To je kritické, pokud jiné vlákno
  nebo proces maže soubory během procházení (např. při promazávání cache).
    - Používá vnitřní iterátor `FileTreeIterator`.
