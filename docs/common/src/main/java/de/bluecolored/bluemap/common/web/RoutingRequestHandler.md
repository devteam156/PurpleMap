# RoutingRequestHandler.java

## Přehled

`RoutingRequestHandler` je `HttpRequestHandler`, který funguje jako router. Umožňuje registrovat jiné handlery pro
specifické cesty (URL paths) pomocí regulárních výrazů.

## Umístění

`de.bluecolored.bluemap.common.web.RoutingRequestHandler`

## Funkcionalita

- Udržuje seznam tras (`Route`).
- **Handle:** Při příchozím požadavku prochází trasy v pořadí (LIFO - poslední přidaná je první kontrolovaná).
- Pokud cesta požadavku odpovídá vzoru trasy (`routePattern`), požadavek je předán příslušnému handleru.
- Před předáním může být cesta požadavku upravena pomocí `replacementRoute` (např. odstranění prefixu).
- Pokud žádná trasa neodpovídá, vrací `400 Bad Request`.

## Metody

### `register(...)`

Registruje novou trasu.

### `handle(HttpRequest request)`

Zpracuje požadavek přesměrováním na odpovídající handler.