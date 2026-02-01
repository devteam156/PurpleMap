# MapSaveTask.java

## Přehled

`MapSaveTask` je atomická úloha, která zajišťuje synchronizaci dat mapy z operační paměti na disk.

## Umístění

`de.bluecolored.bluemap.common.rendermanager.MapSaveTask`

## Implementovaná Rozhraní

- `MapRenderTask`

## Atributy

- `map`: Mapa k uložení.
- `saved`: `AtomicBoolean` zajišťující, že se uložení provede pouze jednou, i kdyby metodu `doWork()` volalo více vláken
  současně.

## Vnitřní Logika a Metody

### `doWork()`

Zavolá `map.save()`, pokud se podaří atomicky změnit `saved` z `false` na `true`.

### `contains(RenderTask task)`

Úloha je považována za shodnou, pokud je to `MapSaveTask` a týká se stejné mapy (podle ID). To brání tomu, aby se ve
frontě hromadilo více požadavků na uložení stejné mapy.
