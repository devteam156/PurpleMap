# Logger.java

## Přehled

`Logger` je abstraktní třída definující rozhraní pro logovací systém v BlueMap. Poskytuje metody pro logování zpráv
různých úrovní (Error, Warning, Info, Debug) a mechanismus pro prevenci zahlcení logu (anti-flood) opakujícími se
zprávami. Také spravuje globální instanci loggeru.

## Umístění

`de.bluecolored.bluemap.core.logger.Logger`

## Balíček

`de.bluecolored.bluemap.core.logger`

## Dědičnost

`java.lang.Object` -> `de.bluecolored.bluemap.core.logger.Logger`
**Implementuje:** `java.lang.AutoCloseable`

## Konstanty a Atributy

### `global`

- **Typ:** `Logger` (konkrétně `MultiLogger`)
- **Popis:** Statická, globálně přístupná instance loggeru. Ve výchozím stavu loguje na standardní výstup (`stdOut()`).
  Aplikace ji může přenastavit nebo do ní přidat další cíle (např. soubor).
- **Inicializace:**
    - Vytvoří se jako `new MultiLogger(stdOut())`.
    - V statickém bloku se registruje **Shutdown Hook**, který při ukončení aplikace zavolá `global.close()`. To zajistí
      správné uzavření souborů a uvolnění zdrojů.

## Abstraktní Metody

Tyto metody musí implementovat konkrétní logger (např. `JavaLogger`, `PrintStreamLogger`).

### `logError(String message, Throwable throwable)`

Zaloguje chybu s volitelnou výjimkou.

### `logWarning(String message)`

Zaloguje varování.

### `logInfo(String message)`

Zaloguje informativní zprávu.

### `logDebug(String message)`

Zaloguje ladicí zprávu (pouze pokud je debug povolen).

### `noFloodError(String key, String message, Throwable throwable)`

Zaloguje chybu, ale pouze pokud zpráva se stejným klíčem `key` nebyla nedávno zalogována. Slouží k potlačení spamu chyb.

### `noFloodWarning(String key, String message)`

Anti-flood verze pro varování.

### `noFloodInfo(String key, String message)`

Anti-flood verze pro info.

### `noFloodDebug(String key, String message)`

Anti-flood verze pro debug.

### `clearNoFloodLog()`

Vymaže historii anti-flood cache (umožní znovu zalogovat dříve potlačené zprávy).

### `removeNoFloodKey(String key)`

Odstraní konkrétní klíč z anti-flood cache.

## Konkrétní Metody (S výchozí implementací nebo pomocné)

### `logError(Throwable throwable)`

- **Popis:** Zjednodušená metoda pro logování výjimky bez vlastní zprávy.
- **Logika:** Volá `logError(throwable.getMessage(), throwable)`.

### `noFloodError(Throwable throwable)`

- **Popis:** Anti-flood logování samotné výjimky. Klíčem pro anti-flood je zpráva výjimky.
- **Logika:** Volá `noFloodError(throwable.getMessage(), throwable)`.

### `noFloodError(String message, Throwable throwable)`

- **Popis:** Anti-flood logování chyby, kde klíč je samotná zpráva.
- **Logika:** Volá `noFloodError(message, message, throwable)`.

### `noFloodWarning(String message)`

- **Popis:** Anti-flood logování varování, klíč je zpráva.
- **Logika:** Volá `noFloodWarning(message, message)`.

### `noFloodInfo(String message)`

- **Popis:** Anti-flood logování infa, klíč je zpráva.
- **Logika:** Volá `noFloodInfo(message, message)`.

### `noFloodDebug(String message)`

- **Popis:** Anti-flood logování debugu, klíč je zpráva.
- **Logika:** Volá `noFloodDebug(message, message)`.

### `removeNoFloodMessage(String message)`

- **Popis:** Odstraní zprávu z anti-flood cache (alias pro `removeNoFloodKey`).
- **Logika:** Volá `removeNoFloodKey(message)`.

### `close()`

- **Popis:** Implementace `AutoCloseable`.
- **Logika:** Výchozí implementace je prázdná.

## Tovární Metody (Static Factory Methods)

### `stdOut()`

- **Návratová hodnota:** `Logger` (`PrintStreamLogger`)
- **Logika:** Vytvoří logger, který píše na `System.out` (info, warning) a `System.err` (error). Debug je vypnutý.

### `stdOut(boolean debug)`

- **Návratová hodnota:** `Logger` (`PrintStreamLogger`)
- **Logika:** Jako `stdOut()`, ale umožňuje zapnout/vypnout debug výstup.

### `file(Path path)`

- **Návratová hodnota:** `Logger`
- **Logika:** Volá `file(path, null)`.

### `file(Path path, boolean append)`

- **Návratová hodnota:** `Logger`
- **Logika:** Volá `file(path, null, append)`.

### `file(Path path, String format)`

- **Návratová hodnota:** `Logger`
- **Logika:** Volá `file(path, format, true)` (append je true).

### `file(Path path, String format, boolean append)`

- **Návratová hodnota:** `Logger` (`JavaLogger` obalující `java.util.logging.Logger`)
- **Logika:**
    1. Vytvoří rodičovské adresáře pro soubor logu (`Files.createDirectories`).
    2. Vytvoří `java.util.logging.FileHandler` pro daný soubor s režimem `append`.
    3. Nastaví formátovač (`LogFormatter`). Pokud je `format` null, použije se výchozí, jinak se použije zadaný
       formátovací řetězec.
    4. Získá instanci anonymního `java.util.logging.Logger`.
    5. Nastaví úroveň na `ALL` a vypne `useParentHandlers` (aby se nelogovalo do konzole, jen do souboru).
    6. Přidá vytvořený `FileHandler` do loggeru.
    7. Vrátí novou instanci `JavaLogger`, která obaluje tento JDK logger.

### `combine(Iterable<Logger> logger)`

- **Návratová hodnota:** `Logger`
- **Logika:** Převede iterable na pole a zavolá `combine(Logger...)`.

### `combine(Logger... logger)`

- **Návratová hodnota:** `Logger`
- **Logika:**
    - Pokud je pole prázdné, vrátí `VoidLogger` (logger, který nic nedělá).
    - Pokud obsahuje jeden logger, vrátí ho přímo.
    - Jinak vrátí `MultiLogger`, který deleguje volání na všechny předané loggery.