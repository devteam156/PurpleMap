# HttpConnection.java

## Přehled

`HttpConnection` spravuje životní cyklus jednoho HTTP spojení (Request -> Response). Implementuje `SelectionConsumer`.

## Umístění

`de.bluecolored.bluemap.common.web.http.HttpConnection`

## Funkcionalita

- **Stav:** Udržuje aktuální `HttpRequest` a `HttpResponse`.
- **Accept (SelectionKey):** Metoda volaná ze smyčky serveru.
    - Čte data ze socketu do `request`.
    - Pokud je request kompletní, předá ho `requestHandler`u (asynchronně v `CompletableFuture`).
    - Jakmile je `futureResponse` hotová, začne zapisovat `response` do socketu.
    - Po odeslání celé odpovědi resetuje stav a čeká na další request (keep-alive) nebo zavře spojení.
- **Asynchronní zpracování:** Vlastní zpracování požadavku (`requestHandler.handle`) běží v odděleném vlákně (
  executoru), aby neblokovalo I/O vlákno serveru.