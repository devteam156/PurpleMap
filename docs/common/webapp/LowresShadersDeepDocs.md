# Lowres Shaders (Image-based 3D)

## Přehled

Nízkorozlišené dlaždice BlueMap jsou rovinné čtverce, které shadery transformují tak, aby vypadaly jako 3D krajina. Tato
technika se nazývá **Displacement Mapping** a umožňuje plynulé zobrazení celého světa s minimální zátěží GPU.

---

# LowresVertexShader.js (GLSL)

## Přehled

Běží pro každý vrchol mřížky nízkorozlišené dlaždice.

## Klíčová Logika: Výšková Transformace

Shader načítá metadata z dolní poloviny PNG textury (viz Lowres Map System) a mění výšku vrcholů:

- **`metaToHeight(meta)`**: Převádí zelený a modrý kanál pixelu zpět na 16bitové číslo představující nadmořskou výšku Y.
- **Deformace:** Nastaví `position.y` na vypočtenou výšku.
- **Anti-Flicker:** Přidává drobný náklon (`- position.x * 0.0001`), aby se zabránilo grafickým artefaktům (Z-fighting)
  v místech, kde se překrývají dvě dlaždice se stejnou výškou.

---

# LowresFragmentShader.js (GLSL)

## Přehled

Zpracovává každý pixel vygenerované plochy a aplikuje komplexní stínování.

## Klíčová Logika: Dynamické efekty

1. **Hires Occlusion (Discard):**
    - **Problém:** Pokud je kamera blízko, hires a lowres vrstvy by se překrývaly a "blikaly".
    - **Řešení:** Shader se podívá do `hiresTileMap` (předané z JavaScriptu). Pokud zjistí, že na dané pozici je již
      načten detailní 3D model, lowres pixel okamžitě zahodí (`discard`). Tím vzniká plynulý přechod mezi 2D a 3D.
2. **Terénní stínování (Slope Shading):**
    - Shader porovná výšku aktuálního pixelu s výškou sousedních pixelů (X+1, Z+1).
    - Rozdíl výšek (`heightDiff`) použije k výpočtu stínu. Stráně odvrácené od pomyslného slunce jsou tmavší, což
      vytváří plastický dojem kopců.
3. **Fake Ambient Occlusion:**
    - Pro první úroveň (LOD 1) shader simuluje AO. Prochází okolí pixelu v malém poloměru a pokud najde vyšší body (
      překážky), pixel ztmaví. Tento efekt se aktivuje pouze při šikmém pohledu kamery.
4. **Osvětlení a Prázdno (Void):**
    - Podobně jako hires shader, míchá blocklight a sunlight.
    - Pokud je pixel průhledný (např. okraj mapy), zamíchá do něj `voidColor` (barvu prázdna) upravenou podle aktuálního
      jasu.
