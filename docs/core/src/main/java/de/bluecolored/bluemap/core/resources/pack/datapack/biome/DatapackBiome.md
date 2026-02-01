# DatapackBiome.java

## Přehled

`DatapackBiome` je implementace rozhraní `Biome`, která čerpá data z načtených JSON souborů v datapacku.

## Umístění

`de.bluecolored.bluemap.core.resources.pack.datapack.biome.DatapackBiome`

## Implementovaná Rozhraní

`Biome`

## Atributy

Obsahuje vnořenou třídu `Data`, která drží:

- `temperature`: Teplota biomu.
- `downfall`: Srážky.
- `effects`: Vizuální efekty (barvy vody, listí, trávy).

## Metody

Všechny metody rozhraní `Biome` (např. `getWaterColor`, `getTemperature`) jsou implementovány tak, že vrací hodnoty z
načtených dat.
