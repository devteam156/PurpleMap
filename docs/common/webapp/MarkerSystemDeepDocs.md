# Frontend Marker System

## Přehled

Balíček `de.bluecolored.bluemap.common.webapp.src.js.markers` implementuje systém pro zobrazování a správu uživatelských
značek. Markery jsou objekty v Three.js scéně, které jsou synchronizovány se souborem `markers.json`.

---

# MarkerManager.js

## Přehled

Základní třída pro správu markerů. Zajišťuje jejich periodické načítání a aktualizaci ze serveru.

## Vnitřní Logika

- **Automatická aktualizace:** Metoda `setAutoUpdateInterval(ms)` nastavuje smyčku pro stahování `markers.json`. BlueMap
  používá inteligentní časování – další požadavek se naplánuje až po dokončení předchozího, aby se předešlo zahlcení
  sítě při pomalém připojení.
- **`updateFromData(data)`**: Abstraktní metoda, kterou implementují konkrétní manažeři (např. `NormalMarkerManager`
  nebo `PlayerMarkerManager`). Převádí JSON data na instance třídy `Marker`.

---

# MarkerSet.js

## Přehled

Kontejnér pro skupinu markerů. V Three.js je to `Scene` (pod-scéna), v uživatelském rozhraní je to položka v menu,
kterou lze zapnout nebo vypnout.

## Vnitřní Logika

- **Hierarchie:** Markery mohou být organizovány do sad (`markerSets`). Sady se mohou rekurzivně větvit.
- **Perzistence:** Stav viditelnosti sady (zda ji uživatel vypnul v menu) se ukládá do `localStorage` prohlížeče. Při
  dalším načtení mapy si BlueMap volbu pamatuje.
- **Factory metoda (`updateMarkerFromData`):** Podle pole `type` v JSONu automaticky vytváří správnou instanci markeru:
    - `poi`: Ikona s textem.
    - `shape`: 2D tvar na zemi.
    - `extrude`: 3D tvar (vytažený do výšky).
    - `line`: Čára (cesta).
    - `html`: Libovolný HTML kód vložený do mapy.

---

# Marker.js (Základní třída)

## Přehled

Základní třída pro všechny typy značek. Dědí od `Three.Object3D`.

## Vnitřní Logika a Matematika

- **Reaktivita:** Všechny základní vlastnosti (pozice, viditelnost, ID) jsou zabaleny do Vue 3 `reactive` objektu. Změna
  pozice markeru v kódu se tak okamžitě projeví v UI (např. v souřadnicích v menu).
- **Vzdálenostní Opacita (`calculateDistanceOpacity`):** BlueMap implementuje automatické mizení markerů, pokud jsou
  příliš blízko nebo příliš daleko od kamery.
    - **Matematika:** Výpočet probíhá projekcí vektoru pozice markeru na vektor směru kamery (`dot product`). Výsledkem
      je kolmá vzdálenost od roviny kamery, nikoli prostá vzdálenost od bodu, což zabraňuje "blikání" markerů na
      okrajích obrazovky.
- **`dispose()`**: Každý marker musí implementovat vyčištění svých zdrojů (geometrie, materiály), aby nedocházelo k
  memory leakům při častých aktualizacích.
