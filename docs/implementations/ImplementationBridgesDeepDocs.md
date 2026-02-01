# Platform Integration Bridges (Fabric, Forge, Sponge)

## Přehled

BlueMap používá architekturu "Abstraktního Pluginu". Většina logiky je v balíčku `common`, zatímco třídy v
`implementations` slouží pouze jako mosty, které implementují rozhraní `Server` a předávají události z herního enginu do
BlueMap.

---

# FabricMod.java & ForgeMod.java

## Přehled

Tyto třídy integrují BlueMap do moderních modovacích rozhraní. Obě implementují rozhraní `Server` a starají se o životní
cyklus módu.

## Vnitřní Logika: Správa výkonu

Jednou z nejdůležitějších funkcí v těchto implementacích je **`updateSomePlayers()`**:

- **Problém:** Pokud je na serveru 100 hráčů, neustálá aktualizace všech pozic v každém ticku by mohla zpomalit hlavní
  vlákno serveru.
- **Řešení:** BlueMap v každém ticku aktualizuje pouze malou část hráčů (`onlinePlayerCount / 20`). To zaručuje, že
  každý hráč je aktualizován zhruba jednou za sekundu, což je pro živou mapu dostatečné, a přitom je dopad na výkon
  serveru zanedbatelný.

## Specifika Platformy

- **Fabric:** Používá `ModInitializer` a registruje události přes Fabric API (např. `ServerTickEvents`).
- **Forge:** Používá systém `@SubscribeEvent` na sběrnici `MinecraftForge.EVENT_BUS`. Speciálně nastavuje
  `IExtensionPoint`, aby Minecraft klient neoznačil server jako nekompatibilní jen proto, že má nainstalovaný BlueMap (
  který je jen na straně serveru).

---

# SpongePlugin.java

## Přehled

Integrace pro SpongePowered API. Využívá Dependency Injection (Guice) pro získání loggerů a cest ke konfiguraci.

## Vnitřní Logika

- **Scheduler:** Na rozdíl od Fabric/Forge, kde si BlueMap tvoří vlastní asynchronní vlákna, Sponge implementace využívá
  nativní `asyncScheduler` enginu pro spouštění renderovacích úloh.
- **Metrics:** Plně integruje systém metrik Sponge, respektuje globální nastavení serveru pro odesílání statistik.

---

# Společné Prvky Bridge tříd

1. **`worlds` cache:** Každá implementace používá `LoadingCache` se slabými klíči (`weakKeys`) pro mapování nativních
   světů enginu na objekty `ServerWorld` v BlueMap. To zajišťuje, že objekty světů v paměti nezůstávají po jejich
   vyložení ze serveru.
2. **`JavaLogger` / `Log4jLogger`**: Adaptéry, které přesměrovávají logy BlueMap do konzole dané platformy se správným
   formátováním.
3. **Command Registration:** Všechny platformy používají `BrigadierBridge` k registraci stejného stromu příkazů
   definovaného v `common`.
