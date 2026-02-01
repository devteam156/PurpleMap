# ResourcePack System

## Přehled

Balíček `de.bluecolored.bluemap.core.resources.pack.resourcepack` zodpovídá za načítání, parsování a "pečení" (baking)
Minecraft ResourcePacků. BlueMap nečte jen jeden soubor, ale dokáže spojit více ResourcePacků dohromady (prioritizace).

---

# ResourcePack.java (Hlavní třída)

## Přehled

Spravuje všechny pooly zdrojů (atlases, blockStates, models, textures, colormaps) a koordinuje jejich načítání.

## Proces Načítání (`loadResources`)

Proces je vysoce paralelní a rozdělený do fází:

1. **Paralelní Load (Fáze 1):** Pomocí `CompletableFuture` a `BlueMap.THREAD_POOL` se současně načítají:
    - **Atlases:** Mapování textur na jejich vlastnosti.
    - **BlockStates:** Pravidla, který model patří ke kterému stavu bloku.
    - **EntityStates:** Pravidla pro modely entit.
    - **Models:** JSON modely (geometrie).
    - **Colormaps:** PNG obrázky pro barvení biomů.
    - **Configs:** Vlastní opravy barev a vlastností bloků dodávané s BlueMap.
2. **Filtrace textur:** BlueMap projde všechny načtené modely a zjistí, které textury jsou skutečně potřeba. Ostatní
   textury z ResourcePacku (např. itemy, UI) ignoruje, čímž šetří RAM.
3. **Bake (Fáze 2):** Po načtení všech souborů následuje proces "pečení":
    - **Texture Baking:** Úprava textur (aplikace atlasů).
    - **Model Optimization:** Převod textových odkazů v modelech na přímé reference.
    - **Parent Application:** Modely v Minecraftu dědí od jiných (např. `cross` -> `flower`). BlueMap rekurzivně spojí
      zděděné vlastnosti.
    - **Property Calculation:** Výpočet, zda je model neprůhledný (occluding) na základě jeho geometrie.

## Rozšíření (Extensions)

`ResourcePack` podporuje systém pluginů. Modely, které vyžadují speciální logiku (např. 3D tráva nebo specifické mody),
mohou registrovat své `ResourcePackExtension`.

---

# BlockState Logic (Balíček blockstate)

Zpracovává soubory v `assets/minecraft/blockstates/*.json`.

### `BlockState.java`

- Rozhoduje mezi dvěma formáty Minecraftu: **Variants** (jednoduchý seznam) a **Multipart** (podmínkové skládání modelu,
  např. u plotů nebo zdí).
- Metoda `forEach(...)`: Pro daný stav bloku ve světě (např. plot se 4 sousedy) vybere všechny odpovídající modely a
  jejich rotace.

### `Variant.java`

- Reprezentuje jeden konkrétní model a jeho transformaci (rotace X, Y a příznak UV-Lock).
- Obsahuje `getTransformMatrix()`: Předvypočtená 4x4 matice pro renderer.

### `BlockStateCondition.java`

- Implementuje logiku pro multipart modely. Dokáže vyhodnotit, zda vlastnosti bloku (např. `north=true`) odpovídají
  podmínce v JSONu.
- Podporuje logické operátory (AND, OR).
