# HttpRequest.java

## Přehled

`HttpRequest` parsuje a uchovává data příchozího HTTP požadavku.

## Umístění

`de.bluecolored.bluemap.common.web.http.HttpRequest`

## Funkcionalita

- **Čtení:** Metoda `write(ReadableByteChannel channel)` (čte z kanálu do bufferu requestu) postupně načítá data.
- **Parsování:**
    - Načítá řádky textu.
    - První řádek parsuje jako `METHOD URI VERSION` (např. `GET /index.html HTTP/1.1`).
    - Další řádky parsuje jako hlavičky (Key: Value).
    - (Implementace těla requestu zatím chybí/je TODO).
- **Atributy:** Poskytuje metody pro získání metody, cesty, GET parametrů, hlaviček a zdrojové IP adresy.

## Metody

### `write(ReadableByteChannel channel)`

Načte data ze socketu. Vrací `true`, pokud je request kompletně načten (hlavičky jsou zpracovány).

### `getGETParams()`

Vrátí mapu parametrů z query stringu URL.