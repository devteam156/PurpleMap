# EntityRenderPass.java

## Přehled

`EntityRenderPass` je implementace `RenderPass` určená pro vykreslování entit do modelu dlaždice.

## Umístění

`de.bluecolored.bluemap.core.map.hires.entity.EntityRenderPass`

## Implementovaná Rozhraní

`RenderPass`

## Funkcionalita

1. Prochází všechny entity v dané oblasti světa (`world.iterateEntities(...)`).
2. Pro každou entitu vytvoří kontext bloku (`BlockNeighborhood`), ve kterém se entita nachází.
3. Zavolá `EntityModelRenderer` pro vygenerování geometrie entity.
4. Posune model entity na správnou pozici v rámci dlaždice.

## Metody

### `render(...)`

Hlavní smyčka přes entity v oblasti.
