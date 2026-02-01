# Render State System

## Přehled

Balíček `de.bluecolored.bluemap.core.map.renderstate` zodpovídá za perzistenci a logiku rozhodování o průběhu
renderování. Uchovává informace o tom, zda se chunky změnily (pomocí hashů) a v jakém stavu se nacházejí jednotlivé
dlaždice (např. vyrenderováno, chyba, mimo hranice).

---

# MapTileState & MapChunkState

## Přehled

Tyto dvě třídy jsou konkrétní implementace `CellStorage`.

- **`MapTileState`**: Spravuje stavy jednotlivých dlaždic (tiles). Používá mřížku 32x32 dlaždic na jednu úložnou buňku (
  region).
- **`MapChunkState`**: Spravuje hashy (timestampy) chunků. Používá mřížku 128x128 chunků na region.

## Vnitřní Logika

Obě třídy využívají bitové posuny (`SHIFT`) pro rychlé určení, do které buňky (souboru na disku) daná souřadnice patří.

- Dlaždice: `x >> 5` (dělení 32).
- Chunky: `x >> 7` (dělení 128).

---

# CellStorage.java (Abstraktní základ)

## Přehled

Generický systém pro ukládání mřížkových dat do souborů (buněk) pomocí BlueNBT. Implementuje LRU cache pro otevřené
buňky.

## Vnitřní Logika

- **Cache:** Používá `LinkedHashMap` s pevnou velikostí (4 buňky). Když se přidá nová buňka a cache je plná, nejstarší
  buňka se automaticky uloží na disk (`saveCell`) a odstraní z paměti.
- **Serializace:** Používá `BlueNBT` s vlastními adaptéry:
    - `RegistryAdapter` pro převod `TileState` na řetězce v NBT.
    - `PalettedArrayAdapter` pro úsporné uložení polí stavů (často se opakují).
- **Samo-léčení (Self-healing):** Pokud je soubor se stavem poškozen (např. chybný formát NBT), BlueMap chybu zaloguje,
  poškozený soubor smaže a vytvoří nový prázdný stav.

---

# TileState.java (Rozhraní / Registr)

## Přehled

Definuje všechny možné stavy, ve kterých se může dlaždice nacházet. Každý stav v sobě nese logiku, jak reagovat na změnu
světa.

## Klíčové Stavy

- **`RENDERED`**: Dlaždice je v pořádku vyrenderovaná.
- **`RENDERED_EDGE`**: Vyrenderovaná dlaždice, která zasahuje do sousedního regionu (potenciálně neúplná).
- **`OUT_OF_BOUNDS`**: Dlaždice je mimo nakonfigurované hranice renderování.
- **`NOT_GENERATED`**: Chunk pod dlaždicí ještě neexistuje.
- **`CHUNK_ERROR`** / **`RENDER_ERROR`**: Nastala chyba při čtení nebo zpracování.

---

# TileActionResolver.java

## Přehled

Toto funkcionální rozhraní definuje "mozek" renderovacího procesu. Na základě aktuálního stavu dlaždice, informace o
změně chunků a situaci s hranicemi rozhodne o další akci.

## Situace Hranic (`BoundsSituation`)

- `INSIDE`: Dlaždice je uvnitř hranic.
- `EDGE`: Dlaždice je na okraji (částečně uvnitř).
- `OUTSIDE`: Dlaždice je zcela mimo.

## Akce (`Action`)

- `NONE`: Nic nedělat.
- `RENDER`: Spustit renderování hires modelu.
- `DELETE`: Smazat existující model z úložiště.

## Rozhodovací Matice (Příklad pro stav RENDERED)

- Pokud je `INSIDE` a chunky se **změnily** -> Akce: `RENDER`, Nový stav: `RENDERED`.
- Pokud je `INSIDE` a chunky se **nezměnily** -> Akce: `NONE`, Nový stav: `RENDERED`.
- Pokud je `OUTSIDE` -> Akce: `DELETE`, Nový stav: `OUT_OF_BOUNDS`.
