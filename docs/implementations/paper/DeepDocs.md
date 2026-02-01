# Paper (Bukkit) Implementation Deep Docs

## Přehled

Balíček `de.bluecolored.bluemap.bukkit` implementuje most mezi BlueMap a servery založenými na Paper/Bukkit API.
Zodpovídá za registraci příkazů, naslouchání událostem (připojení hráčů) a poskytování informací o světech.

---

# BukkitPlugin.java (Hlavní třída)

## Přehled

Hlavní třída pluginu rozšiřující `JavaPlugin`. Implementuje rozhraní `Server` z balíčku Common, čímž BlueMapu umožňuje
dotazovat se na data Minecraft serveru.

## Vnitřní Logika a Životní cyklus

- **`onEnable()`**:
    1. **Folia Check:** Pokud server běží na Folia (vícevláknový Paper), přeskočí vynucené ukládání všech světů (které
       by mohlo způsobit lagy).
    2. **Command Registration:** Používá `BrigadierBridge` k registraci příkazů BlueMap přímo do nativního systému
       Minecraftu. To umožňuje bohatou nápovědu a validaci parametrů přímo v herním chatu.
    3. **Asynchronní Load:** Volá `pluginInstance.load()` v novém vlákně. Tím zajistí, že náročné načítání ResourcePacků
       a inicializace rendereru nezablokuje start serveru.
- **Správa hráčů:**
    - Udržuje cache online hráčů (`onlinePlayerMap`).
    - Každého hráče při připojení zaregistruje do plánovače úloh (Scheduler), který každou sekundu aktualizuje jeho
      pozici pro živou mapu.

---

# FoliaSupport.java

## Přehled

Detekuje, zda server běží na moderním regionálním (vícevláknovém) enginu **Folia**.

## Logika

Pomocí reflexe kontroluje přítomnost třídy `io.papermc.paper.threadedregions.RegionizedServer`. Pokud je nalezena,
BlueMap přepne některé své operace (zejména plánování úloh a přístup ke světům) do režimu kompatibilního s Folia, kde
různé části světa běží v různých vláknech.

---

# EventForwarder.java (Bridge)

## Přehled

Zajišťuje předávání událostí z Bukkitu (např. změna bloku, výbuch, pohyb hráče) do vnitřního systému událostí BlueMap (
`ServerEventListener`).

## Proč je to důležité?

Díky tomuto mostu může BlueMap automaticky detekovat, že byl v určitém regionu položen blok, a naplánovat aktualizaci
příslušné dlaždice v `RenderManager`u, aniž by musela neustále skenovat celé soubory na disku.
