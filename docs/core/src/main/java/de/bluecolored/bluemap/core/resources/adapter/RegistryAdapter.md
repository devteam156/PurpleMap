# RegistryAdapter.java

## Přehled

`RegistryAdapter` je obecný GSON adaptér pro objekty, které jsou spravovány v registru (např. typy bloků, biomů,
rendererů).

## Umístění

`de.bluecolored.bluemap.core.resources.adapter.RegistryAdapter`

## Dědičnost

`TypeAdapter<T>` -> `RegistryAdapter`

## Generika

- `<T extends Keyed>`: Typ objektu v registru. Musí mít klíč.

## Funkcionalita

- **Čtení:** Přečte klíč (řetězec) z JSONu, převede ho na `Key` a vyhledá odpovídající objekt v registru. Pokud objekt
  nenajde, vrátí `fallback` hodnotu a zaloguje varování.
- **Zápis:** Zapíše formátovaný klíč objektu.
