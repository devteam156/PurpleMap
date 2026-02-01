# FabricWorld.java

## Přehled

`FabricWorld` je implementace `ServerWorld` pro Fabric. Obaluje `net.minecraft.server.world.ServerWorld`.

## Umístění

`de.bluecolored.bluemap.fabric.FabricWorld`

## Implementovaná Rozhraní

`ServerWorld`

## Funkcionalita

- **Delegování:** Drží `WeakReference` na serverový svět, aby nebránila jeho uvolnění z paměti.
- **Identifikace:** Získává ID dimenze (`Key`) z registru světa.
- **Ukládání:** Metoda `persistWorldChanges` vyvolá uložení světa (`world.save()`) asynchronně pomocí
  `CompletableFuture` na hlavním vlákně serveru.

## Metody

### `persistWorldChanges()`

Vynutí uložení světa na disk. Důležité pro to, aby BlueMap mohla číst aktuální data z region souborů.

### `getWorldFolder()`

Vrátí cestu k adresáři, kde jsou uložena data světa (regiony).
