# FabricMod.java

## Přehled

`FabricMod` je hlavní třída módu pro Fabric (entrypoint). Implementuje `ModInitializer` a `Server` rozhraní BlueMap.

## Umístění

`de.bluecolored.bluemap.fabric.FabricMod`

## Implementovaná Rozhraní

`ModInitializer`, `Server`

## Funkcionalita

- **Inicializace (`onInitialize`):**
    - Registruje příkazy (pomocí Brigadier).
    - Registruje eventy pro start/stop serveru, připojení/odpojení hráčů a ticky serveru.
    - Spouští načítání BlueMap (`pluginInstance.load()`) v samostatném vlákně po startu serveru.
- **Správa hráčů:** Udržuje seznam online hráčů a periodicky je aktualizuje (`updateSomePlayers`), aby se rozložila
  zátěž.
- **Správa světů:** Udržuje cache `FabricWorld` instancí.
- **Eventy:** Přesměrovává eventy (join/leave) do `FabricEventForwarder`.

## Metody

### `updateSomePlayers()`

Aktualizuje stavy části online hráčů v každém ticku (cca 1/20 hráčů za tick), takže každý hráč je aktualizován jednou za
sekundu. To slouží pro živé aktualizace na webové mapě.
