# BlockStateCondition.java

## Přehled

`BlockStateCondition` je funkcionální rozhraní pro vyhodnocování podmínek v `multipart` definicích bloků.

## Umístění

`de.bluecolored.bluemap.core.resources.pack.resourcepack.blockstate.BlockStateCondition`

## Implementace

- `Property`: Podmínka na přesnou shodu jedné vlastnosti (key=value).
- `PropertySet`: Podmínka na shodu s jednou z možných hodnot (key=v1|v2|v3).
- `And`: Logický součin (AND) více podmínek.
- `Or`: Logický součet (OR) více podmínek.
- `All`: Vždy pravda.
- `None`: Vždy nepravda.

## Metody

### `matches(BlockState state)`

Vrátí `true`, pokud daný `BlockState` splňuje podmínku.

### Tovární metody

Statické metody `and`, `or`, `property` pro pohodlné vytváření podmínek.
