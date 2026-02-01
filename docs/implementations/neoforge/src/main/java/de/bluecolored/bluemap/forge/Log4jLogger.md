# Log4jLogger.java

## Přehled

`Log4jLogger` je implementace `AbstractLogger` pro NeoForge. Přesměrovává logování z BlueMap jádra do standardního Log4j
loggeru používaného v NeoForge.

## Umístění

`de.bluecolored.bluemap.forge.Log4jLogger` (balíček `forge` se používá i pro NeoForge implementaci)

## Dědičnost

`AbstractLogger` -> `Log4jLogger`

## Metody

Implementuje metody `logError`, `logWarning`, `logInfo` a `logDebug` voláním odpovídajících metod `error`, `warn`,
`info`, `debug` na `org.apache.logging.log4j.Logger`.
