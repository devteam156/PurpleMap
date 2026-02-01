# Biome.java

## Přehled

`Biome` je rozhraní reprezentující biom ve světě. Definují se zde barvy vody, listí, trávy a další vlastnosti biomu.

## Umístění

`de.bluecolored.bluemap.core.world.biome.Biome`

## Implementovaná Rozhraní

`Keyed`

## Metody (Vlastnosti)

- `getDownfall()`: Srážky.
- `getTemperature()`: Teplota.
- `getWaterColor()`: Barva vody.
- `getOverlayFoliageColor()`: Barva listí (overlay).
- `getOverlayDryFoliageColor()`: Barva suchého listí.
- `getOverlayGrassColor()`: Barva trávy (overlay).
- `getGrassColorModifier()`: Modifikátor barvy trávy (např. SWAMP, DARK_FOREST).

## Vnořená třída `Default`

Výchozí implementace biomu.
