# Registry.java

## Přehled

`Registry` je generický thread-safe registr pro objekty implementující `Keyed`. Slouží k ukládání a vyhledávání objektů
podle jejich klíče (např. registr typů úloh, registr typů masek).

## Umístění

`de.bluecolored.bluemap.core.util.Registry`

## Atributy

- `entries`: `ConcurrentHashMap<Key, T>` - Vnitřní thread-safe mapa pro uložení prvků.

## Metody

### `register(T entry)`

- **Logika:** Přidá prvek do registru pomocí `putIfAbsent`. Pokud již prvek se stejným klíčem existuje, neudělá nic a
  vrátí `false`. Tím je zajištěna neměnnost registru po první registraci.

### `get(Key key)`

Vrátí prvek s daným klíčem nebo `null`.

### `keys()` / `values()`

Vrací neměnné pohledy na všechny klíče nebo hodnoty v registru.
