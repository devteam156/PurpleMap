# WebFilesManager.java

## Přehled

`WebFilesManager` se stará o správu souborů webové aplikace ve složce webroot.

## Umístění

`de.bluecolored.bluemap.common.WebFilesManager`

## Funkcionalita

- **Extrakce WebApp:** Metoda `updateFiles()` extrahuje soubory webového klienta z `webapp.zip` (uloženého v resources)
  do cílové složky.
- **Správa Nastavení:** Spravuje soubor `settings.json`, který konfiguruje frontend (dostupné mapy, startovní pozice,
  skripty, styly).
- **Synchronizace s Configem:** Umožňuje přenést nastavení z `WebappConfig` do `settings.json` (metody `setFrom`,
  `addFrom`).

## Vnořené třídy

- `Settings`: DTO (Data Transfer Object) reprezentující strukturu `settings.json`.

## Metody

### `updateFiles()`

Aktualizuje soubory frontendu (index.html, js, css...) z resources.

### `saveSettings()` / `loadSettings()`

Pracuje se souborem `settings.json`.

### `addMap(String mapId)`

Přidá mapu do seznamu dostupných map pro frontend.