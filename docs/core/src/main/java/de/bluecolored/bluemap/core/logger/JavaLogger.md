# JavaLogger.java

## Přehled

`JavaLogger` je konkrétní implementace `AbstractLogger`, která funguje jako adaptér pro standardní javovský
`java.util.logging.Logger` (JUL). Umožňuje přesměrovat logování BlueMap do systému, který používá JUL (což je případ
např. `Logger.file`).

## Umístění

`de.bluecolored.bluemap.core.logger.JavaLogger`

## Balíček

`de.bluecolored.bluemap.core.logger`

## Dědičnost

`Logger` -> `AbstractLogger` -> `JavaLogger`

## Atributy

### `out`

- **Typ:** `java.util.logging.Logger`
- **Popis:** Cílový logger, do kterého se budou zprávy předávat.

## Konstruktory

### `JavaLogger(java.util.logging.Logger out)`

- **Parametry:** `out` - logger, do kterého se má zapisovat.
- **Logika:** Uloží instanci loggeru.

## Metody

### `logError(String message, Throwable throwable)`

- **Logika:** Volá `out.log(Level.SEVERE, message, throwable)`. Mapuje BlueMap "Error" na JUL "SEVERE".

### `logWarning(String message)`

- **Logika:** Volá `out.log(Level.WARNING, message)`. Mapuje BlueMap "Warning" na JUL "WARNING".

### `logInfo(String message)`

- **Logika:** Volá `out.log(Level.INFO, message)`. Mapuje BlueMap "Info" na JUL "INFO".

### `logDebug(String message)`

- **Logika:**
    1. Zkontroluje, zda je zapnuté logování pro úroveň `FINE` (`out.isLoggable(Level.FINE)`).
    2. Pokud ano, zaloguje zprávu s úrovní `FINE`. Mapuje BlueMap "Debug" na JUL "FINE".

### `noFloodDebug(String message)` a `noFloodDebug(String key, String message)`

- **Logika:**
    1. Nejdříve zkontroluje `out.isLoggable(Level.FINE)`.
    2. Pokud je debug povolen, zavolá implementaci v předkovi (`super.noFloodDebug`), která provede kontrolu cache.

    - **Důvod:** Optimalizace. Nemá smysl kontrolovat/plnit cache, pokud se debug zprávy stejně nevypisují.

### `close()`

- **Logika:**
    1. Získá všechny handlery připojené k `out` (`out.getHandlers()`).
    2. Pro každý handler zavolá `close()`.

    - Toto je důležité pro zavření souborů (např. když je použit `FileHandler`).