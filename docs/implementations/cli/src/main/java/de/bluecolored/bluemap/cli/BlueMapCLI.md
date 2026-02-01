# BlueMapCLI.java

## Přehled

`BlueMapCLI` je hlavní třída pro příkazovou řádku (Command Line Interface) aplikace BlueMap. Umožňuje spouštět BlueMap
nezávisle na Minecraft serveru (např. pro předgenerování mapy nebo provozování samostatného webserveru).

## Umístění

`de.bluecolored.bluemap.cli.BlueMapCLI`

## Funkcionalita

- **Načítání konfigurace:** Načítá konfigurační soubory z určené složky (defaultně `config/`).
- **Renderování mapy:** Umožňuje spustit renderování mapy (úplné, inkrementální nebo opravu okrajů).
- **Webserver:** Obsahuje integrovaný webserver pro prohlížení mapy.
- **Sledování změn (Watch):** Dokáže sledovat změny v souborech světa a automaticky aktualizovat mapu.
- **Generování webové aplikace:** Extrahuje soubory webového klienta do výstupní složky.

## Metody

### `main(String[] args)`

Vstupní bod aplikace.

1. Parsuje argumenty příkazové řádky pomocí `commons-cli`.
2. Nastavuje logování (soubor, stdout).
3. Načítá konfiguraci a zdroje (resource packy, mody).
4. Inicializuje `BlueMapService`.
5. Spouští požadované akce (renderování, webserver, atd.) na základě přepínačů.

### `renderMaps(...)`

Spustí proces renderování.

1. Načte resource pack.
2. Inicializuje `RenderManager`.
3. Načte nakonfigurované mapy (`BmMap`).
4. Pokud je zapnuto sledování (`watch`), spustí `MapUpdateService` pro každou mapu.
5. Naplánuje úlohy pro renderování map (`MapUpdateTask`).
6. Spustí renderování na pozadí.
7. Pravidelně vypisuje stav (progress) a ukládá mapy.
8. Čeká na dokončení.

### `startWebserver(...)`

Spustí integrovaný webserver.

1. Načte konfiguraci webserveru.
2. Nastaví routování požadavků (`RoutingRequestHandler`).
3. Spustí `HttpServer`.

### `createOptions()`

Definuje dostupné přepínače příkazové řádky:

- `-c, --config`: Cesta ke konfigurační složce.
- `-r, --render`: Spustit renderování.
- `-w, --webserver`: Spustit webserver.
- `-u, --watch`: Sledovat změny souborů.
- `-f, --force-render`: Vynutit kompletní přegenerování.
- `-e, --fix-edges`: Pře-renderovat pouze okraje.
- `-g, --generate-webapp`: Vygenerovat soubory webové aplikace.
- `-s, --generate-websettings`: Aktualizovat pouze `settings.json`.
- `-l, --log-file`: Cesta k souboru s logem.
- `-v, --mc-version`: Verze Minecraftu (pro stažení zdrojů).
- `-m, --maps`: Seznam map k renderování.

## Ošetření chyb

Obsahuje globální `try-catch` blok v metodě `main` pro zachycení chyb konfigurace, chybějících zdrojů nebo I/O chyb.
