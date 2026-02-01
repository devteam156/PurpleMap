# HttpServer.java

## Přehled

`HttpServer` je specializace třídy `Server` pro HTTP protokol.

## Umístění

`de.bluecolored.bluemap.common.web.http.HttpServer`

## Dědičnost

`Server` -> `HttpServer`

## Funkcionalita

- V konstruktoru přijímá `HttpRequestHandler`, který bude zpracovávat požadavky.
- Implementuje metodu `createConnectionHandler()`, která vrací novou instanci `HttpConnection` pro každé spojení.

## Použití

Slouží jako hlavní vstupní bod pro spuštění webového serveru BlueMap.