# BlueMapWorld.java

## Přehled

Rozhraní `BlueMapWorld` reprezentuje herní svět (dimenzi), který byl načten BlueMapou. Jeden svět může mít více map (
`BlueMapMap`), které ho zobrazují (např. různé pohledy, různé renderery).

## Umístění

`de.bluecolored.bluemap.api.BlueMapWorld`

## Metody

### `getId()`

Vrací unikátní identifikátor světa.

### `getSaveFolder()`

**Zastaralé (Deprecated)**
Vrací cestu k adresáři, kde je svět uložen.

- Tato metoda je zastaralá, protože ne všechny světy (v závislosti na platformě a uložení) musí mít fyzickou složku na
  disku ve formátu, který BlueMap očekává.

### `getMaps()`

Vrací kolekci všech map (`BlueMapMap`), které jsou pro tento svět nakonfigurovány a načteny.

- Kolekce je neměnná (unmodifiable).
