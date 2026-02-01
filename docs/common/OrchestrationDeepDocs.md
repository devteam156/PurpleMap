# Orchestration & Integration Logic

## Přehled

Balíček `de.bluecolored.bluemap.common` obsahuje klíčové třídy, které propojují jednotlivé systémy (renderování, web,
konfiguraci) do jednoho funkčního celku.

---

# BlueMapService.java

## Přehled

Tato třída zapouzdřuje veškerou aplikační logiku BlueMap, která je nezávislá na herní platformě. Slouží jako centrální
bod pro správu světů, map a úložišť.

## Vnitřní Logika a Metody

- **Správa map (`loadMap`):**
    - Zodpovídá za správnou interpretaci cest ke světům.
    - Obsahuje **logiku zpětné kompatibility** pro automatickou detekci dimenzí (např. převod složky `DIM-1` na
      `minecraft:the_nether`).
    - Pokud mapa nemá definovaný svět, BlueMap ji považuje za "statickou" (pouze k zobrazení, ne k renderování).
- **Zdroje (Resources):** Koordinuje stahování vanilla Minecraft JARů a následné načítání ResourcePacků a DataPacků.
- **WebFilesManager integration:** Zajišťuje, aby soubory webové aplikace byly vždy v aktuální verzi a synchronizované s
  konfigurací map.

---

# Plugin.java

## Přehled

Hlavní třída pro integraci do Minecraft serverů (Paper, Fabric, Forge). Spravuje životní cyklus (load/unload) a události
serveru.

## Vnitřní Logika: Životní cyklus

- **`load()`**: Kompletní inicializace.
    1. Zablokuje aplikaci pomocí `loadingLock` (aby se zabránilo dvojitému načítání).
    2. Načte konfigurace a doplňky (addons).
    3. Inicializuje `BlueMapService` a `RenderManager`.
    4. **Webserver:** Pokud je zapnutý, vytvoří routování a spustí `HttpServer`.
    5. **Démoni:** Spustí periodické úlohy (automatické ukládání, promazávání cache, sledování změn v souborech světa).
    6. **Player Limit:** Zkontroluje počet hráčů a případně pozastaví renderování pro ušetření výkonu.
- **`unload()`**: Bezpečné vypnutí.
    - Zastaví renderování a počká na dokončení aktuálních úloh (`awaitIdle`).
    - Uloží všechny stavy na disk.
    - Uzavře webserver a síťová spojení.

## Task References

Spravuje krátké náhodné kódy pro úlohy ve frontě, které se používají v příkazech (např. `/bluemap cancel a1b2`).

---

# WebFilesManager.java

## Přehled

Zodpovídá za správu statických souborů webové aplikace v cílovém adresáři (`webroot`).

## Vnitřní Logika

- **`updateFiles()`**: Rozbalí vestavěný `webapp.zip` z JARu do webrootu. Provádí se automaticky při aktualizaci verze.
- **`settings.json`**: Tato třída přímo generuje JSON konfigurační soubor pro JavaScriptový frontend. Překládá nastavení
  z Java objektů `WebappConfig` do formátu, kterému rozumí prohlížeč.

---

# InterruptableReentrantLock.java

## Přehled

Speciální verze zámku (Lock), která BlueMap umožňuje bezpečně přerušit proces načítání.

## Logika

Metoda `interruptAndLock()` se pokusí získat zámek. Pokud jej již drží jiné vlákno (např. zrovna probíhá načítání), toto
vlákno okamžitě přeruší (`interrupt()`) a poté počká, až zámek získá. To je klíčové pro rychlou odezvu příkazu
`/bluemap reload`.
