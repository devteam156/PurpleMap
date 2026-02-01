# RegionType.java

## Přehled

`RegionType` je registr a továrna pro různé formáty regionů (MCA, Linear).

## Umístění

`de.bluecolored.bluemap.core.world.mca.region.RegionType`

## Implementovaná Rozhraní

`Keyed`

## Registry

- `MCA`: Standardní Anvil formát (`.mca`).
- `LINEAR`: Linear formát (`.linear`).

## Metody

### `loadRegion(...)`

Statická metoda, která se pokusí najít a načíst region na daných souřadnicích. Zkouší všechny zaregistrované typy
regionů (zda existuje soubor s příslušnou příponou).

### `forFileName(String fileName)`

Určí typ regionu podle názvu souboru.

### `createRegion(...)`

Vytvoří instanci regionu (`MCARegion` nebo `LinearRegion`).
