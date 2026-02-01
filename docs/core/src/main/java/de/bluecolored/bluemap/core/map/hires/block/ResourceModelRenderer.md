# ResourceModelRenderer.java

## Přehled

`ResourceModelRenderer` je nejdůležitější implementace `BlockRenderer`u. Vykresluje bloky na základě modelů definovaných
v JSON souborech resource packu (standardní Minecraft formát modelů).

## Umístění

`de.bluecolored.bluemap.core.map.hires.block.ResourceModelRenderer`

## Implementovaná Rozhraní

`BlockRenderer`

## Funkcionalita

1. **Získání modelu:** Z varianty bloku získá odkaz na model (`Model`).
2. **Procházení elementů:** Prochází všechny elementy (kvádry), ze kterých se model skládá.
3. **Vytvoření stěn (Faces):** Pro každý element a každou jeho stranu (UP, DOWN, NORTH...) vytvoří geometrii.
4. **Culling (Ořezávání):** Kontroluje, zda má být stěna vykreslena (zda není zakryta sousedním blokem).
5. **Texturování:**
    - Získá texturu z modelu.
    - Vypočítá UV souřadnice (včetně rotace a UV-locku).
6. **Barvení (Tinting):** Aplikuje barvu (tint) na stěnu, pokud je to vyžadováno (např. tráva, listí). Používá
   `BlockColorCalculator`.
7. **Osvětlení:** Aplikuje data o světle (block light, sky light) a ambient occlusion (AO).
8. **Transformace:** Aplikuje transformace modelu (rotace, posun) definované ve variantě nebo vlastnostech bloku (
   náhodný offset).

## Metody

### `render(...)`

Hlavní metoda. Připraví data a volá `buildModelElementResource` pro každý element modelu.

### `buildModelElementResource(...)`

Zpracuje jeden element modelu (cube). Vypočítá jeho rohy a transformace.

### `createElementFace(...)`

Vytvoří geometrii pro jednu stěnu elementu. Zde se děje většina "magie" (světlo, barva, UV, culling).
