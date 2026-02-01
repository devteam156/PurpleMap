# BlockState.java

## Přehled

`BlockState` (v balíčku `resourcepack`) reprezentuje definici vzhledu bloku načtenou ze souboru
`blockstates/<block>.json`.

## Umístění

`de.bluecolored.bluemap.core.resources.pack.resourcepack.blockstate.BlockState`

## Atributy

- `variants`: Mapa variant (pro bloky, které mají různé modely podle stavu, ale vybírá se jen jedna).
- `multipart`: Definice multipart (pro bloky, které se skládají z více částí, které se mohou kombinovat, např. ploty,
  redstone dráty).

## Metody

### `forEach(...)`

Iteruje přes všechny varianty, které platí pro daný stav bloku.

- Pokud má blok `variants`, vybere tu správnou a zavolá pro ni consumer.
- Pokud má blok `multipart`, projde všechny části, zkontroluje podmínky (`when`) a zavolá consumer pro ty, které platí.
