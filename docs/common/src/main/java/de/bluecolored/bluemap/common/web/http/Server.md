# Server.java

## Přehled

`Server` je abstraktní třída implementující základní NIO (Non-blocking I/O) server. Slouží jako základ pro `HttpServer`.

## Umístění

`de.bluecolored.bluemap.common.web.http.Server`

## Dědičnost

`Thread` -> `Server`

## Funkcionalita

- **NIO Selector:** Používá `java.nio.channels.Selector` pro efektivní správu více připojení v jednom vlákně.
- **Bind:** Metoda `bind(SocketAddress)` otevře `ServerSocketChannel` a zaregistruje ho do selectoru pro přijímání
  spojení (`OP_ACCEPT`).
- **Smyčka (run):** V nekonečné smyčce volá `selector.select()` a obsluhuje události (přijetí spojení, čtení, zápis).
- **Akceptace:** Při přijetí nového spojení vytvoří `SelectionConsumer` (pomocí abstraktní metody
  `createConnectionHandler`) a zaregistruje kanál klienta pro čtení a zápis.

## Metody

### `createConnectionHandler()`

Abstraktní metoda, která musí vrátit handler pro nově příchozí spojení (např. `HttpConnection`).