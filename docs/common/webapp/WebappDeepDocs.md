# WebApp Architecture (Frontend)

## Přehled

Frontend BlueMap je moderní webová aplikace (Single Page Application), která využívá GPU uživatele k zobrazení 3D světa.
Je navržena pro vysoký výkon i při milionech trojúhelníků díky efektivnímu streamování dlaždic.

---

# MapViewer.js (Hlavní renderer)

## Přehled

Centrální třída webové aplikace. Spravuje Three.js scénu, renderovací smyčku a propojení mezi 3D světem a Vue UI.

## Vnitřní Logika: Renderovací cyklus

Metoda `renderLoop` běží na frekvenci monitoru (pomocí `requestAnimationFrame`).

1. **Aktualizace Ovládání:** `controlsManager.update()` vypočítá novou pozici kamery.
2. **Ošetření Přesnosti (Precision Fix):**
    - **Problém:** GPU mají omezenou přesnost floatů. Pokud je kamera daleko od bodu 0,0, začne se obraz "třást".
    - **Řešení:** BlueMap pravidelně posouvá celou scénu i kameru zpět k nule (`position.x -= sX`). Tento posun se pak
      kompenzuje v shaderech pomocí uniform proměnných.
3. **Vrstvy Renderování:**
    - **Skybox:** Nejdříve se vykreslí obloha.
    - **Lowres:** Postupně se vykreslují 2D vrstvy od nejvzdálenější (LOD 3) po nejbližší (LOD 1). Mezi vrstvami se maže
      hloubkový buffer, aby nedocházelo k překryvům.
    - **Hires:** Pokud je kamera blízko, vykreslí se detailní 3D modely.
    - **Markers:** Nakonec se vykreslí 3D markery a 2D HTML popisky (`CSS2DRenderer`).

---

# BlueMap.js (Entry Point)

## Přehled

Funguje jako veřejné API frontendu a hlavní exportní soubor. Reexportuje všechny důležité třídy a shadery, aby mohly být
použity v `BlueMapApp.js`.

---

# Technické Detaily Shaderů

BlueMap používá vlastní GLSL shadery pro dosažení specifického Minecraft vzhledu:

- **`HiresVertexShader` / `HiresFragmentShader`**: Zpracovávají binární data z `.prbm` souborů. Aplikují textury, barvy
  biomů a stínování (Ambient Occlusion + Light levels).
- **`LowresVertexShader` / `LowresFragmentShader`**: Zpracovávají PNG dlaždice. Interpretují barevná a výšková data
  zakódovaná v pixelech (viz Lowres Map System) pro dynamické stínování terénu.

---

# Interakce a Raycasting

Metoda `handleMapInteraction` převádí kliknutí na obrazovce na 3D bod v mapě.

1. Převede souřadnice myši na normalizované souřadnice (-1 až 1).
2. Použije `Raycaster` k protnutí paprsku se scénou.
3. Najde nejbližší objekt (blok nebo marker).
4. Pokud má objekt metodu `onClick`, zavolá ji. Tím se spouštějí akce jako otevírání pop-up oken markerů.
5. Vyvolá událost `bluemapMapInteraction`, kterou mohou zachytit externí pluginy.
