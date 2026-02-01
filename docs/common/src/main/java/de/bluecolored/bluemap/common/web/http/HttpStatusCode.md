# HttpStatusCode.java

## Přehled

`HttpStatusCode` je výčet (enum) standardních HTTP stavových kódů.

## Umístění

`de.bluecolored.bluemap.common.web.http.HttpStatusCode`

## Hodnoty

Obsahuje běžné kódy jako:

- `OK` (200)
- `MOVED_PERMANENTLY` (301)
- `BAD_REQUEST` (400)
- `NOT_FOUND` (404)
- `INTERNAL_SERVER_ERROR` (500)
- a další.

## Metody

- `getCode()`: Vrátí číselný kód (int).
- `getMessage()`: Vrátí textovou zprávu (např. "Not Found").