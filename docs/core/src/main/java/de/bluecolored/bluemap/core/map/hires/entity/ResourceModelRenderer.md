# ResourceModelRenderer.java (Entity)

## Přehled

`ResourceModelRenderer` je implementace `EntityRenderer`, která vykresluje části entit na základě modelů z resource
packu.

## Umístění

`de.bluecolored.bluemap.core.map.hires.entity.ResourceModelRenderer`

## Implementovaná Rozhraní

`EntityRenderer`

## Funkcionalita

1. **Model:** Získá model z definice části entity (`Part`).
2. **Elementy:** Prochází elementy modelu (kvádry).
3. **Stěny:** Vytváří geometrii stěn pro každý element.
4. **Světlo a Barva:** Aplikuje osvětlení z bloku, ve kterém entita stojí, a případný tint (barvu).
5. **Transformace:** Aplikuje transformace definované v části entity (např. rotace hlavy, končetin) a transformace
   elementů modelu.

## Metody

### `render(...)`

Hlavní metoda. Vykreslí model entity s aplikovanými transformacemi.

### `buildModelElementResource(...)`

Vytváří geometrii pro jeden element modelu (kvádr).
