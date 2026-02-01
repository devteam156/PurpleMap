# SpongeWorld.java

## Přehled

`SpongeWorld` je implementace `ServerWorld` pro platformu Sponge. Obaluje
`org.spongepowered.api.world.server.ServerWorld`.

## Umístění

`de.bluecolored.bluemap.sponge.SpongeWorld`

## Implementovaná Rozhraní

`ServerWorld`

## Funkcionalita

- **Delegace:** Drží `WeakReference` na Sponge svět.
- **Identifikace dimenze:** Mapuje `WorldType` ze Sponge API na BlueMap klíče.
- **Cesta k souborům:** Zjišťuje kořenový adresář světa. Pokouší se odhadnout strukturu složek (rodičovské složky pro
  Nether/End) na základě adresáře dimenze.
- **Ukládání:** Metoda `persistWorldChanges` vyvolá uložení světa (`delegateWorld.save()`) na synchronním exekutoru
  serveru (hlavní vlákno) pomocí `CompletableFuture`.

## Metody

### `persistWorldChanges()`

Vynutí uložení dat světa na disk.
