# Rotation.java

## Přehled

`Rotation` definuje rotaci elementu v modelu.

## Umístění

`de.bluecolored.bluemap.core.resources.pack.resourcepack.model.Rotation`

## Atributy

- `origin`: Bod, kolem kterého se rotuje.
- `axis`: Osa rotace (X, Y, Z).
- `angle`: Úhel rotace (ve stupních).
- `rescale`: Zda se má element po rotaci zvětšit tak, aby se vešel do původního bounding boxu (používá se velmi zřídka).

## Metody

### `init()`

Vypočítá matici transformace (`MatrixM4f`) odpovídající zadané rotaci.
