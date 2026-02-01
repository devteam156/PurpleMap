# File Storage System

## Přehled

Balíček `de.bluecolored.bluemap.core.storage.file` implementuje rozhraní `Storage` pomocí standardního souborového
systému. Mapy jsou ukládány jako hierarchická struktura složek a souborů.

---

# FileStorage.java

## Přehled

Hlavní instance souborového úložiště. Spravuje kořenový adresář (např. `bluemap/web/maps`) a cachuje instancí
`FileMapStorage` pro jednotlivé mapy.

## Atributy

- `root`: `Path` - Kořenová složka všech map.
- `mapStorages`: `LoadingCache<String, FileMapStorage>` - Cache pro rychlý přístup k úložištím jednotlivých map.

---

# FileMapStorage.java

## Přehled

Implementuje `MapStorage` pro souborový systém. Definuje vnitřní strukturu složek jedné mapy.

## Struktura složek (Layout)

- `tiles/0/`: Hires dlaždice (formát `.prbm`).
- `tiles/{lod}/`: Lowres dlaždice (formát `.png`).
- `rstate/`: Metadata o stavu renderování (`.tiles.dat`, `.chunks.dat`).
- `live/`: Živá data (`markers.json`, `players.json`).
- `assets/`: Textury a modely extrahované pro web.
- `settings.json`: Konfigurace frontendu.

## Vnitřní Logika a Metody

### `delete(DoublePredicate onProgress)`

- **Logika:** Implementuje postupné mazání mapy s reportováním průběhu.
    1. Nejdříve pomocí `FileHelper.walk` sesbírá seznam všech podadresářů a souborů (do hloubky 3).
    2. Postupně maže tyto položky od konce seznamu (nejhlubší první).
    3. Průběžně volá `onProgress.test()` s vypočteným procentem smazaných dat. To umožňuje uživateli mazání zrušit.

---

# FileGridStorage.java

## Přehled

Implementuje `GridStorage`. Ukládá mřížková data (tiles) do souborů s unikátní strukturou, která zabraňuje zpomalení
operačního systému při velkém počtu souborů v jednom adresáři.

## Vnitřní Logika: Adresářová struktura (Hierarchical Layout)

Pokud by BlueMap uložila 1 000 000 dlaždic do jedné složky, většina souborových systémů (NTFS, EXT4) by extrémně
zpomalila.
BlueMap používá **hierarchické kódování cesty**:

- **Příklad:** Souřadnice `x=123, z=-456`
- **Zakódováno:** `x123z-456`
- **Cesta:** `x/1/2/3/z/-/4/5/6.suffix`
- **Logika:** Metoda `getItemPath` rozebere řetězec souřadnic a pro každou číslici (nebo znaménko) vytvoří novou úroveň
  adresáře. Tím je zajištěno, že v žádné složce není více než 10-12 položek (číslice 0-9 a písmena x, z, mínus).

---

# FileItemStorage.java

## Přehled

Implementuje `ItemStorage`. Zajišťuje bezpečný zápis a čtení jednoho konkrétního souboru.

## Vnitřní Logika a Metody

### `write()`

- **Logika:**
    - Pokud je zapnuto `atomic = true`, použije `FileHelper.createFilepartOutputStream`. To znamená, že soubor je zapsán
      jako `.filepart` a až po úspěšném zavření je atomicky přejmenován na cílový název.
    - Tím je zaručeno, že BlueMap nikdy nenechá na disku rozepsaný nebo poškozený soubor (např. při výpadku proudu).
    - Automaticky aplikuje nakonfigurovanou kompresi.

### `read()`

- **Logika:** Vrátí `CompressedInputStream` obalující soubor. Tento stream ví, jak data rozbalit, nebo je může poslat
  komprimovaná přímo webserveru.
