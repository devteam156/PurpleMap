# JsonDataRequestHandler.java

## Přehled

`JsonDataRequestHandler` je jednoduchý handler, který vrací JSON data poskytnutá `Supplier`em.

## Umístění

`de.bluecolored.bluemap.common.web.JsonDataRequestHandler`

## Funkcionalita

- Volá `dataSupplier.get()`.
- Vrací odpověď s `Content-Type: application/json` a `Cache-Control: no-cache`.