# Hires Map System (3D Geometry)

## Přehled

Balíček `de.bluecolored.bluemap.core.map.hires` zodpovídá za generování detailních 3D modelů krajiny. Výsledkem jsou
soubory ve vlastním formátu `.prbm` (Packed Raw BlueMap), které jsou optimalizovány pro přímé nahrání do Vertex Bufferů
v prohlížeči (WebGL/Three.js).

---

# HiresModelManager.java

## Přehled

Hlavní manažer pro hires modely. Koordinuje proces renderování jedné dlaždice pomocí řady renderovacích průchodů (
`RenderPass`).

## Vnitřní Logika a Metody

- **Vláknová bezpečnost:** Používá `ThreadLocal<Collection<RenderPass>>`. Každé renderovací vlákno má svou vlastní sadu
  rendererů, aby se předešlo kolizím a zbytečné synchronizaci.
- **`render(tile, consumer, save)`**:
    1. Vypočítá hranice modelu (`modelMin`, `modelMax`) v blocích.
    2. Získá `ArrayTileModel` z poolu.
    3. Postupně spustí všechny `RenderPass` (např. průchod pro bloky, průchod pro entity).
    4. Výsledný model seřadí podle materiálů (`model.sort()`) – kritické pro výkon GPU.
    5. Uloží model na disk pomocí `PRBMWriter`.

---

# ArrayTileModel.java

## Přehled

Vysoce optimalizovaná paměťová struktura pro ukládání 3D geometrie. Namísto pole objektů používá několik velkých polí
primitivních typů (`float[]`, `byte[]`, `int[]`).

## Struktura Dat (Per Face)

Každý trojúhelník (face) má v polích vyhrazené místo pro:

- `position`: 9 floatů (3 vrcholy * XYZ).
- `uv`: 6 floatů (3 vrcholy * UV souřadnice textury).
- `ao`: 3 floaty (Ambient Occlusion pro každý vrchol).
- `color`: 3 floaty (RGB barva, např. z biomu).
- `sunlight` / `blocklight`: 1 byte (úroveň světla).
- `materialIndex`: 1 int (odkaz do `TextureGallery`).

## Vnitřní Logika

- **`InstancePool`**: Modely se neustále recyklují. Pokud model dlouho nebyl použit nebo je příliš velký, pool ho
  uvolní.
- **`ensureCapacity`**: Pole se dynamicky zvětšují (faktor 1.5x) až do limitu 1 000 000 trojúhelníků.
- **`sort()`**: Seřadí trojúhelníky v polích podle `materialIndex`. To umožňuje prohlížeči vykreslit celou dlaždici
  pomocí minimálního počtu "Draw Calls" (jedno zavolání GPU pro každou texturu).

---

# PRBMWriter.java

## Přehled

Zapisuje `ArrayTileModel` do binárního formátu BlueMap. Formát je navržen tak, aby odpovídal struktuře BufferGeometry v
knihovně Three.js.

## Binární Struktura (.prbm)

1. **Hlavička:** Verze (1 byte), Info bity (1 byte), Počet vrcholů (3 bajty).
2. **Atributy:** Pro každý atribut (position, normal, color, uv, ao...) zapíše:
    - Název (např. "position\0").
    - Typ a formátování (1 byte).
    - Samotná data z polí `ArrayTileModel`.
3. **Normalizace:** Automaticky vypočítává normály ploch (`calculateSurfaceNormal`) a převádí float hodnoty na bajty
   tam, kde je to možné (např. barvy, AO), aby ušetřil místo.
4. **Material Groups:** Na konci souboru je tabulka, která říká: "Materiál ID 5 začíná na vrcholu X a má délku Y".

---

# RenderPass.java (Rozhraní)

Definuje jeden průchod rendererem.

- Metoda `render(world, min, max, anchor, model, consumer)`: Prochází zadanou oblast světa a sype geometrii do
  `TileModel`.
- BlueMap má standardně dva průchody: jeden pro bloky a jeden pro entity.
