# KeyAdapter.java

## Přehled

`KeyAdapter` je GSON adaptér pro třídu `Key` (NamespacedKey).

## Umístění

`de.bluecolored.bluemap.core.resources.adapter.KeyAdapter`

## Dědičnost

`TypeAdapter<Key>` -> `KeyAdapter`

## Funkcionalita

- **Čtení:** Přečte řetězec z JSONu a zparsuje ho na `Key` (formát `namespace:value`).
- **Zápis:** Zapíše `Key` jako formátovaný řetězec.
