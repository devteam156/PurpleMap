# PrintStreamLogger.java

## Přehled

`PrintStreamLogger` je implementace `Logger`, která vypisuje zprávy do zadaných výstupních proudů (`PrintStream`),
typicky `System.out` a `System.err`.

## Umístění

`de.bluecolored.bluemap.core.logger.PrintStreamLogger`

## Dědičnost

`AbstractLogger` -> `PrintStreamLogger`

## Konstruktory

### `PrintStreamLogger(PrintStream out, PrintStream err)`

Vytvoří logger, který píše info/warning na `out` a chyby na `err`. Debug zprávy jsou vypnuté.

### `PrintStreamLogger(PrintStream out, PrintStream err, boolean debug)`

Vytvoří logger s možností povolit debug zprávy.

## Metody

### `logError(...)`

Vypíše zprávu a stacktrace do `err` streamu.

### `logWarning(...)`, `logInfo(...)`

Vypíše zprávu do `out` streamu.

### `logDebug(...)`

Vypíše zprávu do `out` streamu, pouze pokud je `isDebug` nastaveno na `true`.
