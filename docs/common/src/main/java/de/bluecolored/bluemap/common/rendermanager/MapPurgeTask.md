# MapPurgeTask.java

## Přehled

`MapPurgeTask` je destruktivní úloha určená k úplnému vymazání dat mapy z úložiště a resetování jejího vnitřního stavu v
paměti.

## Umístění

`de.bluecolored.bluemap.common.rendermanager.MapPurgeTask`

## Implementovaná Rozhraní

- `MapRenderTask`

## Atributy

- `map`: Mapa, která má být vyčištěna.
- `progress`: Průběh mazání (0.0 až 1.0).
- `hasMoreWork`: Příznak, zda je úkol aktivní.
- `cancelled`: Příznak zrušení.

## Vnitřní Logika a Metody

### `doWork()`

Metoda provádí totální čistku:

1. **Lowres zahození:** Zavolá `map.getLowresTileManager().discard()`, čímž zruší všechny čekající změny v
   nízkorozlišených vrstvách.
2. **Smazání úložiště:** Zavolá `map.getStorage().delete(callback)`. Toto je asynchronní/iterativní proces smazání všech
   souborů dlaždic z disku nebo SQL databáze. Callback průběžně aktualizuje atribut `progress`.
3. **Reset paměti:**
    - `map.resetTextureGallery()`: Vymaže cache textur.
    - `map.getMapTileState().reset()`: Vymaže historii stavů všech dlaždic.
    - `map.getMapChunkState().reset()`: Vymaže historii hashů chunků.
4. Zavolá `map.save()` pro uložení prázdného stavu.

## Poznámka k bezpečnosti

Tato úloha je nevratná. Po jejím dokončení musí BlueMap vyrenderovat celou mapu znovu od nuly.
