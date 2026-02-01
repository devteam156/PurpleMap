# Caches.java

## Přehled

`Caches` poskytuje jednotnou konfiguraci pro cache v celém projektu. Obaluje knihovnu **Caffeine** a integruje ji s
vláknovými pooly BlueMap.

## Umístění

`de.bluecolored.bluemap.core.util.Caches`

## Logika Konfigurace

Metoda `with()` vrací builder s těmito nastaveními:

- **Executor:** `BlueMap.THREAD_POOL` (všechny údržbové operace cache běží na sdíleném poolu).
- **Scheduler:** `BlueMap.SCHEDULER` (pro expiraci podle času).
- **Statistiky:** Automaticky zapíná sběr statistik (`recordStats`).

## Metody

- `build()`: Vytvoří standardní cache s limitem 10 000 položek a expirací 1 minutu od posledního přístupu.
- `build(CacheLoader loader)`: Vytvoří `LoadingCache`, která automaticky načítá data při chybějícím klíči.
