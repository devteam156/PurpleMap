# Element.java

## Přehled

`Element` reprezentuje jeden kvádr (cube) v 3D modelu bloku.

## Umístění

`de.bluecolored.bluemap.core.resources.pack.resourcepack.model.Element`

## Atributy (z JSONu)

- `from`, `to`: Souřadnice protilehlých rohů kvádru (`Vector3f`).
- `rotation`: Rotace elementu (`Rotation`).
- `shade`: Zda má element vrhat stín (ambient occlusion).
- `faces`: Mapa stěn elementu (`EnumMap<Direction, Face>`).

## Metody

### `isFullCube()`

Zkontroluje, zda element vyplňuje celý blok (0,0,0 až 16,16,16) a má definované všechny stěny.

### `optimize(...)`

Deleguje optimalizaci na jednotlivé stěny.
