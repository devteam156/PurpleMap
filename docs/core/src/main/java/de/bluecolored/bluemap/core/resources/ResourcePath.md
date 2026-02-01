# ResourcePath.java

## Přehled

`ResourcePath` je specializovaný klíč (Key), který odkazuje na soubor v resource packu.

## Umístění

`de.bluecolored.bluemap.core.resources.ResourcePath`

## Dědičnost

`Key` -> `ResourcePath<T>`

## Generika

- `<T>`: Typ zdroje, na který cesta odkazuje (např. `Texture`, `Model`).

## Funkcionalita

- Umožňuje "líné" (lazy) načítání a cachování zdroje přímo v objektu cesty.
- Parsování cesty ze souborového systému nebo řetězce.

## Metody

### `getResource(Function<ResourcePath<T>, T> supplier)`

Vrátí odkazovaný zdroj. Pokud ještě nebyl načten (je `null`), použije `supplier` k jeho získání a uloží ho do cache.
