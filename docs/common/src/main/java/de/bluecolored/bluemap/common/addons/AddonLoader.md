# AddonLoader.java

## Přehled

`AddonLoader` se stará o vyhledávání, řešení závislostí a načítání addonů pro BlueMap.

## Umístění

`de.bluecolored.bluemap.common.addons.AddonLoader`

## Funkcionalita

- **Vyhledávání:** Prohledá složku s addony (typicky `addons/` nebo `mods/`).
- **Řešení závislostí:**
    - Odstraní addony, kterým chybí povinné závislosti.
    - Seřadí addony topologicky tak, aby se závislosti načetly dříve než závislé addony.
- **Načítání (`loadAddon`):**
    - Vytvoří `ClassLoader` pro addon. Tento classloader má jako rodiče kombinaci classloaderů všech jeho závislostí (
      `CombinedClassLoader`) a hlavního classloaderu aplikace.
    - Instanciuje hlavní třídu (`entrypoint`).
    - Spustí addon (zavolá `run()`, pokud implementuje `Runnable`).
    - Uloží načtený addon do mapy `loadedAddons`.

## Metody

### `tryLoadAddons(Path root)`

Hlavní metoda pro spuštění procesu načítání ze zadané složky.