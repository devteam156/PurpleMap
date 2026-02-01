# BlueMapService.java

## Přehled

`BlueMapService` je centrální třída, která spojuje konfiguraci, správu souborů, načítání zdrojů (resource packů), světů
a map. Slouží jako hlavní aplikační logika sdílená mezi CLI a pluginovými implementacemi.

## Umístění

`de.bluecolored.bluemap.common.BlueMapService`

## Funkcionalita

- **Správa WebApp:** `createOrUpdateWebApp` aktualizuje soubory webové aplikace a generuje `settings.json`.
- **Načítání Map a Světů:**
    - `getOrLoadMaps`: Načte nakonfigurované mapy.
    - `loadMap`: Načte konkrétní mapu, zinicializuje její svět (`MCAWorld`), úložiště (`Storage`) a resource pack.
    - Řeší automatickou detekci dimenze, pokud není v configu specifikována.
- **Správa Zdroju (Resources):**
    - `getOrLoadResourcePack`: Stáhne (pokud je třeba) vanilla zdroje pro danou verzi MC a načte je spolu s resource
      packy a mody ze složek.
    - `loadDataPack`: Načte datapacky světa.
    - `getPackRoots`: Sestaví seznam cest, odkud se mají načítat zdroje (vanilla, mody, resource packy, extensions).
- **Správa Úložišť:** `getOrLoadStorage` inicializuje a cachuje úložiště mapových dlaždic (SQL/File).
- **Verze Minecraftu:** `getOrLoadMinecraftVersion` zajistí stažení manifestu verzí a potřebných jar souborů z Mojang
  serverů (pokud je povoleno).

## Metody

### `getOrLoadMaps(...)`

Hlavní metoda pro získání map. Prochází konfiguraci a načítá mapy, které ještě nejsou v paměti.

### `createOrUpdateWebApp(...)`

Zajišťuje, že ve složce webroot jsou aktuální soubory klienta a vygenerovaný konfigurační soubor pro frontend.

### `close()`

Zavře všechna otevřená úložiště.