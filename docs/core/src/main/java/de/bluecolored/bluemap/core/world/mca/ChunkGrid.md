# ChunkGrid.java

## Přehled

`ChunkGrid` spravuje načítání a cachování chunků a regionů v mřížce.

## Umístění

`de.bluecolored.bluemap.core.world.mca.ChunkGrid`

## Funkcionalita

- **Mřížka:** Definuje mřížku chunků a regionů (16x16 chunků, 32x32 chunků v regionu).
- **Cache:** Používá `LoadingCache` (Caffeine) pro cachování načtených regionů a chunků.
    - Cache regionů drží otevřené soubory regionů.
    - Cache chunků drží parsovaná data chunků.
- **Načítání:** Deleguje načítání chunků na `Region` a `ChunkLoader`.
- **Preload:** Umožňuje přednačíst všechny chunky v regionu (optimalizace pro sekvenční renderování).

## Metody

### `getChunk(int x, int z)`

Získá chunk na daných souřadnicích (z cache nebo načtením).

### `preloadRegionChunks(...)`

Iteruje přes všechny chunky v regionu a vloží je do cache.

### `listRegions()`

Vrátí seznam souřadnic všech regionů, které existují na disku.