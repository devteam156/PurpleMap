# LogFormatter.java

## Přehled

`LogFormatter` je vlastní implementace `java.util.logging.Formatter`. Definuje, jakým způsobem se budou formátovat
zprávy logované do souboru (pomocí `JavaLogger` a `FileHandler`).

## Umístění

`de.bluecolored.bluemap.core.logger.LogFormatter`

## Balíček

`de.bluecolored.bluemap.core.logger`

## Dědičnost

`java.util.logging.Formatter` -> `LogFormatter`

## Atributy

### `format`

- **Typ:** `String`
- **Popis:** Formátovací řetězec kompatibilní s `java.util.Formatter` (printf).

## Konstruktory

### `LogFormatter()`

- **Logika:** Volá druhý konstruktor s výchozím formátem: `"[%1$tF %1$tT][%4$s] %5$s%6$s%n"`.
    - `%1$tF %1$tT`: Datum a čas (ISO 8601).
    - `[%4$s]`: Úroveň logu (Severity).
    - `%5$s`: Samotná zpráva.
    - `%6$s`: Stacktrace chyby (pokud existuje).
    - `%n`: Odřádkování.

### `LogFormatter(String format)`

- **Logika:** Uloží předaný formátovací řetězec.

## Metody

### `format(LogRecord record)`

- **Popis:** Převede `LogRecord` (záznam o jedné logované události) na `String`.
- **Logika:**
    1. **Datum:** Převede `record.getInstant()` na `ZonedDateTime` v systémové časové zóně.
    2. **Zdroj (Source):** Určí původce zprávy.
        - Pokud je vyplněno `sourceClassName`, použije ho (případně přidá `sourceMethodName`).
        - Jinak použije název loggeru (`record.getLoggerName()`).
    3. **Zpráva:** Zformátuje samotný text zprávy voláním `formatMessage(record)` (to řeší např. lokalizaci nebo
       parametry ve zprávě).
    4. **Výjimka (Throwable):**
        - Pokud `record.getThrown()` není null (obsahuje výjimku), vytvoří `StringWriter` a `PrintWriter`.
        - Vypíše stacktrace výjimky do writeru.
        - Výsledek převede na string.
        - Pokud výjimka není, použije prázdný řetězec.
    5. **Finální formátování:** Zavolá `String.format` s uloženým `format` řetězcem a parametry:
        1. `zdt` (Datum)
        2. `source` (Zdroj - třída/metoda)
        3. `record.getLoggerName()` (Jméno loggeru)
        4. `record.getLevel().getLocalizedName()` (Název úrovně - INFO, WARNING...)
        5. `message` (Zpráva)
        6. `throwable` (Stacktrace)
    6. Vrátí výsledný řetězec.