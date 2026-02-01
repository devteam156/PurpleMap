# MultiLogger.java

## Přehled

`MultiLogger` je implementace `Logger`, která umožňuje sdružovat více loggerů dohromady. Zpráva zalogovaná do
`MultiLogger` je předána všem podřízeným loggerům.

## Umístění

`de.bluecolored.bluemap.core.logger.MultiLogger`

## Dědičnost

`AbstractLogger` -> `MultiLogger`

## Funkcionalita

- Udržuje mapu podřízených loggerů.
- Je thread-safe (používá `ReentrantReadWriteLock`).
- Umožňuje dynamicky přidávat a odebírat loggery za běhu.

## Metody

### `put(Logger logger)`

Přidá logger pod automaticky vygenerovaným názvem.

### `put(String name, LoggerSupplier loggerSupplier)`

Přidá logger pod zadaným názvem. Pokud logger se stejným názvem již existuje, je nejprve odstraněn (a uzavřen).

### `remove(String name)`

Odebere a uzavře logger se zadaným názvem.

### `clear()`

Odebere a uzavře všechny podřízené loggery.

### Logovací metody (`logError`, `logInfo`...)

Předají zprávu všem aktivním podřízeným loggerům.
