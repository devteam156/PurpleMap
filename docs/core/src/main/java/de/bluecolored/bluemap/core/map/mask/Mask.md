# Mask.java

## Přehled

`Mask` je rozhraní definující obecnou oblast v 3D prostoru, která má být renderována.

## Umístění

`de.bluecolored.bluemap.core.map.mask.Mask`

## Konstanty

- `NONE`: Prázdná maska (nic se nerenderuje).
- `ALL`: Plná maska (vše se renderuje).

## Metody

### `test(int x, int y, int z)`

Základní metoda: je bod uvnitř masky?

### `test(int minX, int minY, int minZ, int maxX, int maxY, int maxZ)`

Optimalizovaná metoda: je oblast uvnitř masky?

- `TRUE`: Celá uvnitř.
- `FALSE`: Celá venku.
- `UNDEFINED`: Částečně uvnitř nebo neznámo.

### `isEdge(...)`

Určuje, zda je daná oblast na hraně masky. Pokud ano, renderování může označit dlaždici jako "edge" (pro pozdější
přegenerování při změně masky).

### `submask(...)`

Vrátí masku optimalizovanou pro danou podoblast.

### `inverted()`

Vrátí inverzní masku (to, co bylo uvnitř, je venku a naopak).
