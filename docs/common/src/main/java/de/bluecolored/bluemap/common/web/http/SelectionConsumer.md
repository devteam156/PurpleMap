# SelectionConsumer.java

## Přehled

`SelectionConsumer` je funkcionální rozhraní, které rozšiřuje `Consumer<SelectionKey>`. Používá se v `Server` třídě pro
zpracování událostí ze `Selector`u.

## Umístění

`de.bluecolored.bluemap.common.web.http.SelectionConsumer`

## Funkcionalita

Definuje metodu `accept(SelectionKey key)`, která se zavolá, když je kanál připraven k I/O operaci.