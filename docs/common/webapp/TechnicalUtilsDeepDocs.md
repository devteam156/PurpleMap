# WebApp Technical Utilities

## Přehled

Balíček `de.bluecolored.bluemap.common.webapp.src.js.util` obsahuje nízkoúrovňové třídy, které rozšiřují možnosti
Three.js a zajišťují správnou synchronizaci mezi 3D scénou a DOMem prohlížeče.

---

# CombinedCamera.js

## Přehled

Nejdůležitější třída pro plynulý uživatelský zážitek. Umožňuje plynule přecházet mezi **Perspektivní kamerou** (3D
pohled) a **Ortografickou kamerou** (2D plochá mapa).

## Vnitřní Logika: Interpolace Projekce

Standardní Three.js kamery neumí měnit svůj typ za běhu bez "skoku". `CombinedCamera` to řeší lineární interpolací
matic:

1. **Dvě Matice:** Udržuje v paměti `perspectiveProjection` a `ortographicProjection`.
2. **`ortho` parametr:** Číslo od 0.0 (3D) do 1.0 (2D).
3. **Výpočet:** V metodě `updateProjectionMatrix()` vypočítá výslednou matici jako vážený průměr obou matic na základě
   parametru `ortho`.
4. **Křivka:** Pro přirozenější pocit nepoužívá lineární váhu, ale mocninnou funkci (`-pow(ortho - 1, 6) + 1`), což dělá
   přechod na konci velmi jemným.

---

# CSS2DRenderer.js

## Přehled

Umožňuje vložit standardní HTML elementy (např. popisky markerů, tlačítka) do 3D scény tak, aby se "vznášely" nad
příslušnými body na mapě.

## Vnitřní Logika

- **Synchronizace:** Renderer neustále přepočítává 3D pozici objektu na 2D pozici na obrazovce (`project`).
- **Transformace:** Místo nastavování `top/left` používá CSS transformaci `translate(-50%, -50%)`, což je mnohem
  plynulejší, protože to prohlížeč počítá na GPU.
- **Z-Order (Hloubka):**
    - **Problém:** HTML je vždy nad 3D plátnem.
    - **Řešení:** Renderer vypočítá vzdálenost objektu od kamery a nastaví mu odpovídající `z-index`. Objekty, které
      jsou dál, mají nižší index a jsou opticky "za" těmi bližšími. Pokud je objekt za kamerou (`vector.z > 1`),
      automaticky se skryje (`display: none`).

---

# RevalidatingFileLoader.js & RevalidatingTextureLoader.js

## Přehled

Speciální loadery, které řeší problém s cachováním souborů na straně prohlížeče.

## Logika

Když BlueMap zjistí, že byla mapa aktualizována, tyto loadery přidávají k URL náhodný parametr (cache-buster), ale
dělají to inteligentně – pouze pro soubory, o kterých ví, že se mohly změnit. To zajišťuje, že uživatel vidí aktuální
mapu bez nutnosti tvrdého obnovení stránky (F5).
