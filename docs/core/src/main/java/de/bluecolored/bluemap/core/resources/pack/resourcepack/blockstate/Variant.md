# Variant.java

## Přehled

`Variant` reprezentuje jednu konkrétní variantu vzhledu bloku v souboru blockstate. Odkazuje na model a definuje jeho
transformace.

## Umístění

`de.bluecolored.bluemap.core.resources.pack.resourcepack.blockstate.Variant`

## Atributy (z JSONu)

- `model`: Cesta k modelu (`models/*.json`).
- `x`, `y`, `z`: Rotace modelu podle os (ve stupních).
- `uvlock`: Zda se má textura "uzamknout" při rotaci modelu (aby se netočila s ním).
- `weight`: Váha pro náhodný výběr (pokud existuje více variant).

## Atributy (Runtime)

- `renderer`: Typ rendereru, který se má použít (např. `DEFAULT`, `LIQUID`).
- `transformed`: Zda má varianta nějakou transformaci.
- `transformMatrix`: Předpočítaná matice transformace (posun a rotace).

## Metody

### `init()`

Metoda volaná po deserializaci (`@PostDeserialize`). Vypočítá transformační matici.

- Posune model tak, aby střed rotace byl ve středu bloku (0.5, 0.5, 0.5).
- Aplikuje rotace.
- Posune model zpět.
