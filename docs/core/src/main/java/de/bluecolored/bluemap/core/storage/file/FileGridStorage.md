# FileGridStorage.java

## Přehled

`FileGridStorage` je implementace `GridStorage`, která ukládá data do souborového systému. Používá stromovou strukturu
adresářů pro efektivní ukládání velkého množství souborů (dlaždic) na základě jejich souřadnic (x, z).

## Umístění

`de.bluecolored.bluemap.core.storage.file.FileGridStorage`

## Implementovaná Rozhraní

`GridStorage`

## Struktura adresářů

Cesta k souboru je generována metodou `getItemPath`. Souřadnice x a z jsou zakódovány do řetězce (např. `x10z-5`) a
tento řetězec je rozdělen po znacích na adresáře. To zabraňuje tomu, aby v jednom adresáři bylo příliš mnoho souborů.
Příklad: `x/1/0/z/-5/x10z-5.json.gz`

## Metody

### `getItemPath(int x, int z)`

Generuje cestu k souboru na základě souřadnic.

### `stream()`

Iteruje přes všechny soubory v úložišti. Prochází adresářovou strukturu a parsuje názvy souborů zpět na souřadnice.

### `write(...)`, `read(...)`, `delete(...)`

Deleguje operace na `FileItemStorage` (který vytvoří pro danou buňku).
