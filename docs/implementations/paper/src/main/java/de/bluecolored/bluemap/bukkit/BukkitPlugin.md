# BukkitPlugin.java

## Přehled

`BukkitPlugin` je hlavní třída pluginu pro Paper (entrypoint).

## Umístění

`de.bluecolored.bluemap.bukkit.BukkitPlugin`

## Implementovaná Rozhraní

`Server`, `Listener`

## Funkcionalita

- **Inicializace (`onEnable`):**
    - Registruje eventy.
    - Uloží světy (aby se vygeneroval `level.dat`).
    - Registruje příkazy (pomocí Paper Brigadier API).
    - Inicializuje `onlinePlayerMap` a spouští pravidelnou aktualizaci hráčů.
    - Spouští načítání BlueMap v novém vlákně.
    - Startuje bStats metriky.
- **Správa hráčů:**
    - `initPlayer`: Vytvoří `BukkitPlayer` a naplánuje pro něj periodickou úlohu (`runAtFixedRate`) pro aktualizaci
      dat (pozice atd.).
    - Na Folia/Paperu se používá regionální plánovač, takže každý hráč je aktualizován v kontextu své entity/regionu.
- **API:** Poskytuje přístup k `BukkitWorld` a dalším serverovým funkcím.

## Metody

### `onEnable()` / `onDisable()`

Životní cyklus pluginu.

### `initPlayer(...)`

Inicializuje sledování hráče. Používá `player.getScheduler().runAtFixedRate` pro kompatibilitu s Folia (úloha běží na
vlákně, které vlastní entitu hráče).
