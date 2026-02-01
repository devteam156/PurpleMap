# MCAWorldRegionWatchService.java

## Přehled

`MCAWorldRegionWatchService` sleduje změny v souborech regionů (`.mca`) ve složce světa pomocí
`java.nio.file.WatchService`.

## Umístění

`de.bluecolored.bluemap.core.world.mca.MCAWorldRegionWatchService`

## Implementovaná Rozhraní

`WatchService<Vector2i>`

## Funkcionalita

- Registruje `WatchService` na složce s regiony.
- Sleduje události `ENTRY_CREATE`, `ENTRY_MODIFY`, `ENTRY_DELETE`.
- Převádí změněné soubory na souřadnice regionů (`Vector2i`).
- Metody `poll()` a `take()` vracejí seznam souřadnic regionů, které se změnily.

## Metody

### `poll()` / `take()`

Získává události ze služby sledování.

### `ensureInitialization()`

Zajistí, že je sledování aktivní (zaregistruje složku, pokud existuje).