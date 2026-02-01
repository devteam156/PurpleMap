# BlueMapAPI.java

## Přehled

`BlueMapAPI` je hlavní vstupní bod pro interakci s BlueMap. Poskytuje přístup k mapám, světům, rendereru, webové
aplikaci a dalším komponentám. API je navrženo jako thread-safe (bezpečné pro vlákna) a může být voláno asynchronně.

## Umístění

`de.bluecolored.bluemap.api.BlueMapAPI`

## Získání instance

Instanci API nelze vytvořit přímo. Je nutné použít statické metody pro registraci posluchačů (listenerů) nebo získání
volitelné instance.

### `getInstance()`

Statická metoda, která vrací `Optional<BlueMapAPI>`. Pokud je BlueMap načtena a povolena, obsahuje instanci API. Jinak
je prázdná.

### `onEnable(Consumer<BlueMapAPI> consumer)`

Zaregistruje posluchače, který bude zavolán, jakmile bude BlueMapAPI povoleno a připraveno k použití.

- Pokud je API již povoleno, posluchač se zavolá okamžitě (synchronně).
- Posluchač může být zavolán opakovaně (např. při reloadu pluginu).
- Volání obvykle probíhá asynchronně (mimo hlavní vlákno serveru).

### `onDisable(Consumer<BlueMapAPI> consumer)`

Zaregistruje posluchače, který bude zavolán těsně před vypnutím nebo reloadem BlueMap.

### `unregisterListener(Consumer<BlueMapAPI> consumer)`

Odregistruje dříve přidaného posluchače.

## Hlavní metody API

### `getRenderManager()`

Vrací `RenderManager` pro ovládání vykreslování.

### `getWebApp()`

Vrací `WebApp` pro interakci s webovým rozhraním (skripty, styly, hráči).

### `getPlugin()`

Vrací `Plugin` rozhraní pro konfiguraci pluginu (skiny, ikony).

### `getMaps()`

Vrací kolekci všech načtených `BlueMapMap`.

### `getWorlds()`

Vrací kolekci všech načtených `BlueMapWorld`.

### `getWorld(Object world)`

Získá `BlueMapWorld` na základě identifikátoru světa.

- `world` může být: ID (String), UUID, Path, nebo objekt světa z platformy (org.bukkit.World, ServerWorld atd.).

### `getMap(String id)`

Získá `BlueMapMap` podle jejího ID.

### `getBlueMapVersion()`

Vrací verzi BlueMap.

### `getAPIVersion()`

Vrací verzi BlueMap API.
