# Part.java

## Přehled

`Part` definuje jednu část entity (např. tělo, hlava, končetina). Odkazuje na model a definuje jeho pozici a rotaci.

## Umístění

`de.bluecolored.bluemap.core.resources.pack.resourcepack.entitystate.Part`

## Atributy (z JSONu)

- `model`: Cesta k modelu části.
- `position`: Posun části (Vector3f).
- `rotation`: Rotace části (Vector3f).

## Atributy (Runtime)

- `renderer`: Typ rendereru (např. `DEFAULT`).
- `transformed`: Zda má část transformaci.
- `transformMatrix`: Matice transformace.

## Metody

### `init()`

Vypočítá transformační matici z pozice a rotace.
