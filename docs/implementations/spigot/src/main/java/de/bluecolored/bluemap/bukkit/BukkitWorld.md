# BukkitWorld.java

## Přehled

`BukkitWorld` je implementace `ServerWorld` pro platformu Spigot/Bukkit. Obaluje instanci `org.bukkit.World`.

## Umístění

`de.bluecolored.bluemap.bukkit.BukkitWorld`

## Implementovaná Rozhraní

`ServerWorld`

## Funkcionalita

- **Identifikace dimenze:** Mapuje prostředí světa (`Environment`) na klíče BlueMap (overworld, the_nether, the_end).
- **Cesta k souborům:** Určuje cestu k adresáři dimenze (region soubory). Řeší nestandardní strukturu složek na Bukkit
  serverech (kde dimenze nemusí být vnořené).
- **Ukládání:** Metoda `persistWorldChanges` vyvolá uložení světa (`world.save()`) synchronně na hlavním vlákně
  serveru (pomocí `BukkitScheduler`).

## Metody

### `persistWorldChanges()`

Vynutí uložení dat světa na disk. Volá `delegateWorld.save()` na hlavním vlákně a čeká na dokončení.
