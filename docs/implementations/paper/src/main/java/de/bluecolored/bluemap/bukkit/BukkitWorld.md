# BukkitWorld.java

## Přehled

`BukkitWorld` je implementace `ServerWorld` pro Bukkit/Paper. Obaluje instanci `org.bukkit.World`.

## Umístění

`de.bluecolored.bluemap.bukkit.BukkitWorld`

## Implementovaná Rozhraní

`ServerWorld`

## Funkcionalita

- **Identifikace dimenze:** Mapuje prostředí světa (`Environment`) na BlueMap klíče (`overworld`, `the_nether`,
  `the_end`). Pro vlastní dimenze používá jejich klíč.
- **Cesta k souborům:** Zjišťuje cestu k datům dimenze. Řeší specifika Bukkitu, kde `worldFolder` může být přímo složka
  dimenze, zatímco BlueMap očekává standardní strukturu `level.dat` + `DIM-1` atd.
- **Ukládání:** Metoda `persistWorldChanges` vyvolá uložení světa (`world.save()`).
    - Na Folia je toto volání přeskočeno (není bezpečné volat save z libovolného vlákna nebo globálně).
    - Na Paperu se uložení naplánuje na hlavní vlákno serveru.

## Metody

### `persistWorldChanges()`

Vynutí uložení dat světa na disk.
