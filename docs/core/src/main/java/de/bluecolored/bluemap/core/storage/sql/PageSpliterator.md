# PageSpliterator.java

## Přehled

`PageSpliterator` je implementace `Spliterator` pro líné (lazy) načítání dat po stránkách (batchích). Používá se pro
iterování nad velkými sadami dat z databáze bez nutnosti načíst vše do paměti najednou.

## Umístění

`de.bluecolored.bluemap.core.storage.sql.PageSpliterator`

## Generika

- `<T>`: Typ prvků ve streamu.

## Konstruktor

Přijímá `IntFunction<T[]> pageSupplier`, což je funkce, která pro dané číslo stránky (0, 1, 2...) vrátí pole prvků.

## Metody

### `tryAdvance(Consumer<? super T> action)`

Zpracuje jeden prvek.

- Pokud je v aktuálním batchi (`lastBatch`) ještě prvek, vrátí ho.
- Pokud batch došel, načte další stránku pomocí `pageSupplier`.
- Pokud `pageSupplier` vrátí prázdné pole nebo null, iterace končí.

### `trySplit()`

Pokusí se rozdělit iterátor pro paralelní zpracování. V této implementaci vrátí spliterator pro zbývající prvky v
aktuálním batchi a sám se posune na konec batche (takže další volání `tryAdvance` načte novou stránku).
