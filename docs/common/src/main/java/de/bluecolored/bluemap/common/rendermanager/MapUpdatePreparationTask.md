# MapUpdatePreparationTask.java

## Přehled

`MapUpdatePreparationTask` je přípravná úloha, která předchází samotnému renderování mapy. Jejím úkolem je projít
soubory světa (a případně existující mapy), identifikovat regiony, které vyžadují pozornost, a sestavit z nich sekvenci
konkrétních renderovacích úloh. Tato úloha se obvykle spouští při startu serveru nebo při ručním vyvolání
`/bluemap update`.

## Umístění

`de.bluecolored.bluemap.common.rendermanager.MapUpdatePreparationTask`

## Balíček

`de.bluecolored.bluemap.common.rendermanager`

## Implementovaná Rozhraní

- `MapRenderTask`

## Atributy

- `map`: Cílová mapa.
- `center`, `radius`: Volitelné parametry pro omezení aktualizace na kruhovou oblast.
- `force`: Strategie vynucení updatu.
- `taskConsumer`: Callback (typicky `renderManager::scheduleRenderTask`), který přijme výslednou složenou úlohu.

## Vnitřní Logika a Metody

### `doWork()`

Provádí lineární proces přípravy:

1. **Vyhledání regionů (`findRegions`):** Sestaví množinu souřadnic regionů (`Vector2i`), které mají být zpracovány.
2. **Vytvoření úloh (`createTasks`):** Převede nalezené regiony na seznam `WorldRegionRenderTask`.
3. **Odeslání:** Vytvoří `MapUpdateTask` a předá ji do `taskConsumer`.

### `findRegions()`

Tato metoda obsahuje sofistikovanou vyhledávací logiku:

1. **Skenování světa:** Projde všechny soubory regionů v adresáři světa (`world.listRegions()`).
2. **Filtrování:**
    - Odstraní regiony mimo `render-boundaries` (nastaveno v configu mapy).
    - Pokud je zadán `radius`, provede kruhovou filtraci (počítá vzdálenost středu regionu od středu oblasti).
3. **Detekce smazaných oblastí:**
    - Pokud je v nastavení mapy povoleno `checkForRemovedRegions`, BlueMap prohledá i složku s uloženými daty mapy (
      tile-state soubory).
    - Hledá regiony, které mají uložený stav jiný než `UNKNOWN` nebo `NOT_GENERATED`, ale které už neexistují v
      souborech světa.
    - Tyto regiony přidá do seznamu k updatu, aby proces renderování mohl tyto dlaždice korektně smazat (`DELETE` akce).

### `createTasks(Collection<Vector2i> regions)`

1. Vytvoří seznam `WorldRegionRenderTask` pro všechny nalezené regiony.
2. **Řazení:** Seřadí úlohy pomocí `WorldRegionRenderTask.defaultComparator(Vector2i.ZERO)`. To zajistí, že se mapa
   renderuje od souřadnic 0,0 směrem ven, což je pro uživatele vizuálně nejlepší.
3. **Obalení:** Do seznamu přidá `MapSaveTask` na začátek i na konec, aby se zajistilo uložení konzistentního stavu
   mapy.

## Konstrukce a Builder

Třída používá Lombok `@Builder` pro flexibilní vytváření instancí. Poskytuje také statické metody `updateMap(...)` jako
zjednodušené entrypointy pro běžné scénáře.
