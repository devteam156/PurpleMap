# BlockNeighborhood.java

## Přehled

`BlockNeighborhood` je specializovaný `ExtendedBlock`, který poskytuje efektivní přístup k sousedním blokům v malém
okolí (neighborhood).

## Umístění

`de.bluecolored.bluemap.core.world.block.BlockNeighborhood`

## Dědičnost

`ExtendedBlock` -> `BlockNeighborhood`

## Funkcionalita

- Udržuje cache pro bloky v okolí 8x8x8 (diameter 8).
- Umožňuje rychle získat sousední bloky pomocí `getNeighborBlock`.
- Automaticky načítá a kopíruje data bloků do pole `neighborhood` při posunu "středového" bloku.

## Metody

### `getNeighborBlock(int dx, int dy, int dz)`

Vrátí objekt `ExtendedBlock` pro sousední blok. `dx, dy, dz` jsou relativní souřadnice.
