# CoreConfig.java

## Přehled

`CoreConfig` obsahuje globální nastavení jádra BlueMap, které ovlivňuje výkon, ukládání dat a sběr statistik. Odpovídá
souboru `core.conf`.

## Umístění

`de.bluecolored.bluemap.common.config.CoreConfig`

## Atributy

### `acceptDownload`

- **Typ:** `boolean` (Výchozí: `false`)
- **Popis:** Zda uživatel souhlasí se stahováním externích zdrojů (vanilla Minecraft JARy) z Mojang serverů. Nutné pro
  fungování.

### `renderThreadCount`

- **Typ:** `int` (Výchozí: `1`)
- **Popis:** Počet vláken pro renderování.
- **Logika:** Pokud je hodnota `<= 0`, vypočítá se jako `pocet_jader + hodnota` (např. -1 na 4jádru vytvoří 3 vlákna).

### `renderThreadPriority`

- **Typ:** `int` (Výchozí: `5` - NORM_PRIORITY)
- **Popis:** Priorita vláken v OS (1 až 10).

### `metrics`

- **Typ:** `boolean` (Výchozí: `true`)
- **Popis:** Povolení odesílání anonymních statistik o používání.

### `data`

- **Typ:** `Path` (Výchozí: `bluemap`)
- **Popis:** Cesta ke složce, kam BlueMap ukládá své vnitřní soubory (resources, logy).

### `scanForModResources`

- **Typ:** `boolean` (Výchozí: `true`)
- **Popis:** Zda má BlueMap prohledávat složku s mody a pokoušet se z nich extrahovat textury a modely.

### `log`

- **Typ:** `LogConfig` (Vnitřní třída)
- **Popis:** Nastavení logování do souboru.
    - `file`: Cesta k souboru (např. `logs/debug.log`).
    - `append`: Zda přidávat do existujícího souboru (`true`) nebo ho přepsat (`false`).

## Metody

### `resolveRenderThreadCount()`

- **Logika:** Převádí konfigurovanou hodnotu (včetně záporných čísel pro relativní počet k CPU) na finální kladné číslo
  vláken. Vždy vrátí alespoň 1.