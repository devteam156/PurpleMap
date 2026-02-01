# Frontend Shader & Binary Loader

## Přehled

Tato sekce popisuje, jak BlueMap interpretuje binární formát `.prbm` a jak používá vlastní GLSL shadery k věrnému
zobrazení Minecraft světa v prohlížeči.

---

# PRBMLoader.js (Binární parser)

## Přehled

Parser pro formát **PRBM** (Packed Raw BlueMap). Je to vysoce optimalizovaný formát založený na PRWM, který umožňuje
přímé nahrání geometrie do grafické karty bez zbytečného parsování textu (jako u JSON nebo OBJ).

## Vnitřní Logika: Dekódování

- **Endianness:** Automaticky detekuje, zda systém uživatele používá Little-Endian nebo Big-Endian, a v případě potřeby
  data za běhu přerovná (`copyFromBuffer`).
- **Atributy:** Prochází binární bloky a vytváří `Three.BufferAttribute`. Typicky:
    - `position`: Pozice vrcholů.
    - `normal`: Směry stěn (pro stínování).
    - `color`: Barvy z biomů.
    - `uv`: Souřadnice textur.
    - `ao`, `sunlight`, `blocklight`: Vlastní atributy BlueMap pro osvětlení.
- **Material Groups:** Přečte tabulku skupin na konci souboru a nastaví je objektu `BufferGeometry`. To umožňuje
  renderovat jednu dlaždici s desítkami různých textur jediným průchodem (pokud jsou správně seřazeny).

---

# HiresVertexShader.js (GLSL)

## Přehled

Běží na GPU pro každý vrchol geometrie.

## Klíčová Logika: Směrové Osvětlení

Shader implementuje dynamické stínování, které zvýrazňuje 3D strukturu bloků:

- **`lightDirection`**: Fixní vektor světla (1.0, 0.5).
- **Výpočet:** Pomocí skalárního součinu (`dot product`) normály stěny a směru světla vypočítá ztmavení.
- **Vzdálenostní útlum:** Efekt se plynule vytrácí (`smoothstep`), pokud je kamera příliš daleko, což šetří výkon a
  zabraňuje vizuálnímu šumu.

---

# HiresFragmentShader.js (GLSL)

## Přehled

Běží na GPU pro každý pixel na obrazovce.

## Klíčová Logika: Míchání barev a Animace

1. **Animované Textury:** Shader vypočítá aktuální pozici v textuře na základě času a metadat animace (
   `animationFrameIndex`). Podporuje i lineární interpolaci mezi snímky pro plynulé efekty (např. tekoucí voda).
2. **Osvětlení (Light Logic):**
    - Kombinuje `vSunlight` a `vBlocklight` na základě globálního parametru `sunlightStrength` (den/noc).
    - Výsledek míchá s `ambientLight` (minimální jas).
3. **Ambient Occlusion:** Vynásobí výslednou barvu hodnotou `vAo` (stíny v rozích).
4. **Chunk Borders:** Pokud je zapnuto v nastavení, shader matematicky vypočítá vzdálenost pixelu od hranice 16x16 bloků
   a přimaluje fialovou linku. To vše probíhá čistě v shaderu bez nutnosti měnit geometrii.
5. **Průhlednost:** Pixely s alfou nižší než 0.01 jsou okamžitě zahozeny (`discard`), což zajišťuje ostré výřezy (listí,
   mříže).
