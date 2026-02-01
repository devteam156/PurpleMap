# CommandSet.java

## Přehled

`CommandSet` je rozhraní, které definuje sadu operací nad SQL databází. Odděluje logiku úložiště od konkrétního SQL
dialektu.

## Umístění

`de.bluecolored.bluemap.core.storage.sql.commandset.CommandSet`

## Implementovaná Rozhraní

`Closeable`

## Metody

Definuje metody pro:

- Inicializaci tabulek.
- Práci s položkami (`ItemStorage`): zápis, čtení, mazání.
- Práci s mřížkou (`GridStorage`): zápis, čtení, mazání, výpis.
- Správu map: mazání celé mapy, výpis ID map.
