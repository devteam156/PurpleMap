# Server.java

## Přehled

`Server` je rozhraní, které abstrahuje serverovou platformu (implementaci). Poskytuje BlueMap přístup k informacím o
serveru, světům, hráčům a konfiguraci.

## Umístění

`de.bluecolored.bluemap.common.serverinterface.Server`

## Metody

### `getMinecraftVersion()`

Vrací verzi Minecraftu běžící na serveru.

### `getConfigFolder()`

Vrací cestu k adresáři s konfigurací pluginu.

### `getModsFolder()`

Vrací volitelnou cestu k adresáři s mody (pro načítání textur z modů).

### `isMetricsEnabled()`

Umožňuje serveru přepsat nastavení metrics (např. globální zákaz v konfiguraci serveru).

### `getServerWorld(World world)`

Najde odpovídající `ServerWorld` pro daný `World` z jádra BlueMap (MCAWorld). Používá cache pro optimalizaci.

### `getServerWorld(Object world)`

Najde `ServerWorld` pro libovolný objekt světa (např. `org.bukkit.World`).

### `getLoadedServerWorlds()`

Vrací kolekci všech aktuálně načtených světů na serveru.

### `getOnlinePlayers()`

Vrací kolekci online hráčů (`Player`).

### `registerListener(ServerEventListener listener)`

Zaregistruje posluchače událostí serveru (připojení/odpojení hráče).

### `unregisterAllListeners()`

Odregistruje všechny posluchače.
