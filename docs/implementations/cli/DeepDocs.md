# CLI Implementation Deep Docs

## Přehled

Balíček `de.bluecolored.bluemap.cli` implementuje rozhraní pro příkazovou řádku. Umožňuje plnohodnotné využití všech
funkcí BlueMap (renderování, webserver, správa markerů) v prostředí bez GUI, typicky na dedikovaných serverech nebo v
Docker kontejnerech.

---

# BlueMapCLI.java (Hlavní entry point)

## Přehled

Zpracovává parametry příkazové řádky a koordinuje spouštění služeb.

## Klíčové Funkce a Logika

### 1. Zpracování parametrů (Apache Commons CLI)

Metoda `main` definuje bohatou sadu přepínačů:

- `-r` (render): Spustí jednorázové renderování map.
- `-w` (webserver): Spustí vestavěný HTTP server.
- `-u` (watch): Po vyrenderování zůstane běžet a sleduje změny v souborech světa.
- `-f` (force): Vynutí kompletní přegenerování mapy.
- `-c` (config): Určuje cestu ke složce s konfigurací (výchozí `./config`).

### 2. Správa renderování (`renderMaps`)

Tato metoda implementuje workflow pro CLI renderování:

1. **Webapp:** Pokud je povoleno, vygeneruje/aktualizuje soubory webové aplikace v cílové složce.
2. **Resources:** Stáhne a načte ResourcePacky.
3. **Filtrace:** Umožňuje omezit renderování pouze na vybrané mapy (přes `-m`).
4. **Sledování (Info Task):** Spouští periodický úkol, který každých 10 sekund vypisuje do konzole aktuální postup (%) a
   **ETA (odhadovaný čas dokončení)**.
5. **Shutdown Hook:** Registruje speciální vlákno (`shutdownHook`), které při násilném ukončení (Ctrl+C) zajistí
   bezpečné uložení rozpracovaných dat a korektní uzavření souborů.

### 3. Sledování souborů (`watch` režim)

Pokud je aktivován příznak `-u`, CLI verze po dokončení hlavního renderu nespustí ukončení, ale zinicializuje
`MapUpdateService` pro každou mapu. Tato služba reaguje na změny v souborech `.mca` (Anvil) a automaticky přidává
změněné regiony do fronty `RenderManager`u.

### 4. Webserver režim

CLI verze může fungovat jako čistý webový server. Metoda `startWebserver` nastavuje routování podobně jako v pluginové
verzi, ale s logováním přímo do standardního výstupu (při zapnutém `-b`).

## Exit Kódy

- `0`: Úspěšné dokončení.
- `1`: Obecná chyba (chyba v konfiguraci, IO chyba).
- `2`: Chybějící zdroje (uživatel neakceptoval stahování Minecraft JARu).
