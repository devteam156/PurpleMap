# PackVersion.java

## Přehled

`PackVersion` reprezentuje verzi formátu balíčku (Resource Pack nebo Data Pack). Skládá se z hlavního čísla (`major`) a
vedlejšího čísla (`minor`, zavedeno v pozdějších verzích MC).

## Umístění

`de.bluecolored.bluemap.core.resources.pack.PackVersion`

## Atributy

- `major`: Hlavní číslo verze.
- `minor`: Vedlejší číslo verze (volitelné, výchozí 0).

## Metody

### `isGreaterOrEqual(PackVersion other)`

Porovná verze. Vrátí `true`, pokud je tato verze větší nebo rovna `other`.

### `isSmallerOrEqual(PackVersion other)`

Porovná verze. Vrátí `true`, pokud je tato verze menší nebo rovna `other`.

## Vnořené třídy (Adaptéry)

- `Adapter`: GSON adaptér pro serializaci/deserializaci. Podporuje čtení verze jako čísla (int nebo double), řetězce ("
  1.2") nebo pole ([1, 2]).
- `MinAdapter`, `MaxAdapter`: Specializované adaptéry pro čtení rozsahů verzí (pokud verze chybí, použije se 0 nebo
  MAX_INT).
