# Block Rendering System

## Přehled

Balíček `de.bluecolored.bluemap.core.map.hires.block` obsahuje logiku pro převod jednotlivých bloků na trojúhelníky.
Systém je postaven na renderovacích průchodech a specializovaných rendererech pro různé typy bloků (standardní,
kapaliny).

---

# BlockRenderPass.java

## Přehled

Implementuje jeden kompletní průchod renderéru přes oblast bloků.

## Vnitřní Logika: Sloupcové renderování

Pro každý horizontální bod (X, Z) v mřížce dlaždice:

1. **Zjištění výšky:** Projde vertikální sloupec bloků odshora dolů (`maxY` -> `minY`).
2. **Renderování bloku:** Pro každý blok zavolá `blockRenderer.render()`.
3. **Míchání barev:** Výsledná barva bloku se přimíchá k barvě sloupce pomocí `underlay` (protože jdeme odshora).
4. **Optimalizace (RenderTopOnly):** Pokud je blok zcela neprůhledný a zakrývá své sousedy, renderer ukončí průchod
   tímto sloupcem (protože nic pod tímto blokem již není vidět).
5. **Lowres report:** Na konci sloupce pošle výslednou barvu, nejvyšší výšku a úroveň světla do `tileMetaConsumer` (pro
   lowres dlaždice).

---

# BlockStateModelRenderer.java

## Přehled

Zprostředkovatel mezi stavem bloku a konkrétním rendererem.

## Vnitřní Logika

- **Waterlogging:** Pokud je blok označen jako `waterlogged`, renderer nejdříve vyrenderuje samotný model bloku a poté
  nad něj (pomocí `overlay`) vyrenderuje model vody.
- **Varianty:** Pro každý blok zjistí z ResourcePacku seznam variant modelu. Pro každou variantu pak vybere správný
  renderer (např. `ResourceModelRenderer`) a spojí jejich geometrii.

---

# ResourceModelRenderer.java

## Přehled

Nejdůležitější renderer. Interpretuje standardní Minecraft JSON modely.

## Vnitřní Logika: Tvorba geometrie

1. **Elementy:** Prochází pole `elements` v JSON modelu (např. krychle, desky).
2. **Stěny (Faces):** Pro každou ze 6 stěn krychle:
    - **Culling:** Zkontroluje, zda stěna sousedí s jiným neprůhledným blokem. Pokud ano, stěnu vůbec nevytváří (šetří
      tisíce trojúhelníků).
    - **Ambient Occlusion (AO):** Pokud je AO zapnuto, metoda `testAo` zkontroluje 4 sousední bloky kolem každého
      vrcholu. Podle počtu překážek (occluding blocks) nastaví vrcholu stín (0.25 až 1.0).
    - **UV-Lock:** Pokud je model variantou otočen, renderer provede protisměrnou rotaci UV souřadnic, aby textura na
      bloku zůstala zarovnaná se světem (jako v Minecraftu).
    - **Tinting:** Pokud má stěna `tintindex`, použije `BlockColorCalculator` k získání barvy biomu.

---

# LiquidModelRenderer.java

## Přehled

Renderer specializovaný na vodu a lávu. Na rozdíl od pevných bloků dynamicky mění výšku vrcholů.

## Vnitřní Logika

- **Dynamická hladina:** Metoda `getLiquidCornerHeight` vypočítá průměrnou výšku hladiny v každém rohu bloku na základě
  úrovně (`level`) okolních 4 bloků kapalin.
- **Tekoucí textury:**
    - Pokud se hladina svažuje, renderer vypočítá úhel toku (`getFlowingAngle`).
    - Poté aplikuje rotaci na UV souřadnice a použije texturu `flow` místo `still`.
- **Optimalizace:** Kapaliny se nerenderují, pokud jsou zcela pod neprůhledným blokem.
