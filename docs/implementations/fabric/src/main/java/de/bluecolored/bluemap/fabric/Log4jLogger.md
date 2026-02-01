# Log4jLogger.java

## Přehled

`Log4jLogger` je implementace `AbstractLogger`, která přesměrovává logování z BlueMap jádra do Log4j, což je standardní
logger v prostředí Fabric (a Minecraftu).

## Umístění

`de.bluecolored.bluemap.fabric.Log4jLogger`

## Dědičnost

`AbstractLogger` -> `Log4jLogger`

## Metody

Přepisuje metody `logError`, `logWarning`, `logInfo` a `logDebug` tak, aby volaly odpovídající metody na instanci
`org.apache.logging.log4j.Logger`.
