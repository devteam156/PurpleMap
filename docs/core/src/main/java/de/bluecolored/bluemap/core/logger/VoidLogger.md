# VoidLogger.java

## Přehled

`VoidLogger` je "prázdná" implementace `Logger`, která nedělá nic. Všechny logovací metody jsou prázdné.

## Umístění

`de.bluecolored.bluemap.core.logger.VoidLogger`

## Dědičnost

`Logger` -> `VoidLogger`

## Použití

Používá se jako "null object" nebo placeholder tam, kde je vyžadován logger, ale žádný výstup není žádoucí (např. při
testování nebo vypnutém logování).
