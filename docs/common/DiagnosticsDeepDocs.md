# Diagnostics & Metrics

## Přehled

Balíček `de.bluecolored.bluemap.common` obsahuje nástroje pro monitorování běhu aplikace. Nejdůležitějšími komponentami
jsou `StateDumper`, který umožňuje "vyfotit" kompletní vnitřní stav BlueMap, a `Metrics`, který odesílá anonymní data o
verzích.

---

# StateDumper.java (Komplexní diagnostika)

## Přehled

`StateDumper` je extrémně výkonný nástroj pro debugging. Dokáže rekurzivně projít všechny důležité instance objektů v
paměti a vyexportovat je do formátu JSON.

## Vnitřní Logika: Deep Introspection

Metoda `dump(Path file)` provádí hloubkovou analýzu:

1. **System Info:** Sbírá data o OS, verzi Javy, počtu jader CPU a využití RAM.
2. **Thread Dump:** Prochází všechna běžící vlákna a pro každé z nich vypíše StackTrace.
3. **Instance Reflection:** Prochází všechny registrované objekty (např. `Plugin`, `RenderManager`).
    - **Rekurze:** Pomocí reflexe prochází všechna pole objektů. Aby se vyhnul nekonečné smyčce, udržuje si
      `IdentityHashMap` již navštívených objektů.
    - **Caffeine Integration:** Pokud narazí na cache, automaticky do JSONu přidá její statistiky (hit-rate, eviction
      count atd.).
    - **Anotace:** Podporuje vlastní anotaci `@DebugDump`, kterou lze pole explicitně zahrnout nebo vyloučit z výpisu.

## Použití

Tento výstup je neocenitelný při hlášení chyb, kdy vývojář vidí přesný stav všech rendererů, front úloh a konfiguračních
parametrů v momentě problému.

---

# Metrics.java (Anonymní statistiky)

## Přehled

Jednoduchý systém pro odesílání informací o používání BlueMap.

## Vnitřní Logika

- **Data:** Odesílá pouze tři informace: typ implementace (např. "paper"), verzi BlueMap a verzi Minecraftu.
- **Přenos:** Data jsou odesílána asynchronně přes HTTPS POST na centrální server BlueMap.
- **Zabezpečení:** Nepřenáší se žádné IP adresy, názvy světů ani seznamy hráčů. Proces je plně v souladu s ochranou
  soukromí a lze jej vypnout v konfiguraci.
