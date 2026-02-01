# CellStorage.java

## Přehled

`CellStorage` je abstraktní třída, která implementuje systém ukládání dat "buněk" (cells) do `GridStorage`. Používá se
pro ukládání stavu renderování (`MapTileState`, `MapChunkState`). Data jsou serializována pomocí `BlueNBT` (formát NBT).

## Umístění

`de.bluecolored.bluemap.core.map.renderstate.CellStorage`

## Generika

- `<T extends CellStorage.Cell>`: Typ buňky, kterou toto úložiště spravuje.

## Funkcionalita

- **Caching:** Udržuje `LinkedHashMap` načtených buněk (LRU cache).
- **Persistence:** Načítá a ukládá buňky do `GridStorage` (komprimované streamy).
- **BlueNBT:** Používá knihovnu BlueNBT pro (de)serializaci objektů buněk.

## Metody

### `cell(int x, int z)`

Získá buňku na daných souřadnicích (načte z cache nebo disku, případně vytvoří novou).

### `save()`

Uloží všechny změněné buňky z cache na disk.

### `loadCell(Vector2i pos)`

Načte buňku ze souboru. Pokud soubor je poškozený, pokusí se ho smazat a vytvořit novou buňku.

### `saveCell(Vector2i pos, T cell)`

Uloží buňku, pokud byla modifikována (`cell.isModified()`).
