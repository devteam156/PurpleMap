# Log4jLogger.java

## Přehled

`Log4jLogger` je implementace `AbstractLogger`, která přesměrovává logování z BlueMap jádra do Log4j loggeru používaného
v prostředí Forge.

## Umístění

`de.bluecolored.bluemap.forge.Log4jLogger`

## Dědičnost

`AbstractLogger` -> `Log4jLogger`

## Metody

Implementuje metody `logError`, `logWarning`, `logInfo` a `logDebug` voláním odpovídajících metod `error`, `warn`,
`info`, `debug` na `org.apache.logging.log4j.Logger`.
