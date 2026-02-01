# ForgeWorld.java

## Přehled

`ForgeWorld` je implementace `ServerWorld` pro NeoForge. Obaluje instanci `net.minecraft.server.level.ServerLevel`.

## Umístění

`de.bluecolored.bluemap.forge.ForgeWorld`

## Implementovaná Rozhraní

`ServerWorld`

## Funkcionalita

- **Delegace:** Drží `WeakReference` na `ServerLevel`, aby se zabránilo únikům paměti.
- **Uložení:** Metoda `persistWorldChanges` vyvolá asynchronní uložení světa (`world.save()`) na hlavním vlákně serveru.
- **Cesta:** Určuje cestu k adresáři světa pomocí `server.getWorldPath(LevelResource.ROOT)`.

## Metody

### `persistWorldChanges()`

Vynutí uložení dat světa na disk, aby BlueMap mohla číst aktuální data.

### `getWorldFolder()`

Vrací cestu k adresáři s daty světa.
