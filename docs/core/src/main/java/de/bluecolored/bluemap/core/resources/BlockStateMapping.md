# BlockStateMapping.java

## Přehled

Generická třída pro mapování hodnot (např. vlastností bloku nebo barevných funkcí) na konkrétní stavy bloku.

## Umístění

`de.bluecolored.bluemap.core.resources.BlockStateMapping`

## Funkcionalita

- Drží `BlockState` (klíč) a mapovanou hodnotu `T`.
- Metoda `fitsTo(BlockState blockState)` zjišťuje, zda se předaný blok shoduje s klíčem. Shoda nastane, pokud předaný
  blok má stejné ID a **všechny** vlastnosti definované v klíči mají stejnou hodnotu. (Vlastnosti navíc nevadí).