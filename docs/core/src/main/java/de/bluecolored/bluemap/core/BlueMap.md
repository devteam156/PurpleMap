# BlueMap.java

## Přehled

`BlueMap` je hlavní třída jádra (core) celé aplikace. Slouží jako centrální bod pro přístup ke globálním konstantám,
verzování a sdíleným vláknovým poolům. Tuto třídu využívají všechny ostatní moduly (API, Common, Implementace) pro
získání základních informací o běhovém prostředí BlueMap.

## Umístění

`de.bluecolored.bluemap.core.BlueMap`

## Balíček

`de.bluecolored.bluemap.core`

## Dědičnost

`java.lang.Object` -> `de.bluecolored.bluemap.core.BlueMap`

## Konstanty a Atributy

### `VERSION`

- **Typ:** `String`
- **Popis:** Verze aplikace BlueMap (např. "3.5.0" nebo "DEV"). Tato hodnota je načtena ze souboru `version.json` v
  resources. Pokud načtení selže nebo je hodnota zástupný znak (`${version}`), nastaví se na "DEV".

### `GIT_HASH`

- **Typ:** `String`
- **Popis:** Zkrácený hash commitu z Gitu, ze kterého byla aplikace sestavena. Slouží pro přesnější identifikaci verze
  při ladění. Stejně jako verze se načítá z `version.json`.

### `THREAD_POOL`

- **Typ:** `java.util.concurrent.ForkJoinPool`
- **Popis:** Globální sdílený pool vláken pro paralelní zpracování úloh (např. renderování dlaždic, IO operace).
- **Konfigurace:**
    - Počet vláken odpovídá počtu dostupných procesorů (`Runtime.getRuntime().availableProcessors()`).
    - Používá vlastní `ForkJoinWorkerThreadFactory`, která:
        - Vytváří nová vlákna.
        - Nastavuje **Context ClassLoader** vlákna na ClassLoader třídy `BlueMap`. Toto je **kritické** pro
          kompatibilitu s platformami jako Forge, kde různé mody běží v izolovaných ClassLoaderech. Bez tohoto by vlákna
          nemusela vidět třídy BlueMap nebo Minecraftu.
        - Nastavuje jméno vlákna ve formátu `BlueMap-FJP-{index}`.
    - Režim `asyncMode` je vypnutý (`false`), což je standard pro výpočetní úlohy (LIFO zpracování úloh v rámci vlákna).

### `SCHEDULER`

- **Typ:** `java.util.concurrent.ScheduledExecutorService`
- **Popis:** Globální plánovač pro periodické nebo odložené úlohy (např. aktualizace metrik, kontrola změn souborů).
- **Konfigurace:**
    - Používá pool o velikosti 1 vlákna (`Executors.newScheduledThreadPool(1, ...)`).
    - Používá továrnu na vlákna, která:
        - Vytváří virtuální (platform) vlákna s názvem `BlueMap-Scheduler-`.
        - Stejně jako u `THREAD_POOL` nastavuje **Context ClassLoader** na ClassLoader třídy `BlueMap` pro zajištění
          kompatibility.

## Statický Inicializační Blok (Static Initializer)

Tento blok se provede při prvním načtení třídy `BlueMap` do paměti. Jeho úkolem je načíst verzi a git hash.

**Logika:**

1. Definuje výchozí hodnoty pro `version` a `gitHash` na "DEV".
2. Pokusí se načíst soubor `/de/bluecolored/bluemap/version.json` z classpath.
    - Používá `GsonConfigurationLoader` (knihovna Configurate) pro parsování JSONu.
3. Pokud se načtení podaří:
    - Získá hodnotu `version` z uzlu "version". Pokud v JSONu chybí, použije "DEV".
    - Získá hodnotu `git-hash` z uzlu "git-hash". Pokud chybí, použije "DEV".
4. Pokud dojde k `IOException` (soubor neexistuje nebo nejde přečíst), zaloguje chybu pomocí `Logger.global.logError` a
   ponechá výchozí hodnoty.
5. Provede kontrolu "placeholderů":
    - Pokud načtená verze je doslovně `"${version}"` (což se stává v neošetřeném vývojovém prostředí před nahrazením
      Gradle buildem), změní ji zpět na "DEV".
    - Totéž pro `"${gitHash}"`.
6. Přiřadí finální hodnoty do veřejných konstant `VERSION` a `GIT_HASH`.

## Metody

Třída neobsahuje žádné veřejné metody, slouží pouze jako kontejner pro statické konstanty a zdroje.
