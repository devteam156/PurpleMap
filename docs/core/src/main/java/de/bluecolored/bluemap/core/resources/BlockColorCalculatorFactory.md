# BlockColorCalculatorFactory.java

## Přehled

Tato třída spravuje logiku pro výpočet barev bloků (tráva, listí, voda, redstone). Načítá konfigurace z
`blockColors.json`.

## Umístění

`de.bluecolored.bluemap.core.resources.BlockColorCalculatorFactory`

## Funkcionalita

- **Načítání (`load`):** Parsuje JSON mapování bloků na funkce barev (např. `@foliage`, `@grass`, nebo hex kód barvy).
- **Colormapy:** Metody `setFoliageMap`, `setGrassMap` atd. načítají obrázky colormap do polí `int[]` pro rychlý
  přístup.
- **Kalkulátor:** Metoda `createCalculator()` vrátí instanci vnitřní třídy `BlockColorCalculator`, která provádí samotné
  výpočty.

## Vnitřní třída `BlockColorCalculator`

Provádí výpočty barev pro konkrétní blok v kontextu (neighborhood).

- `getBlended...Color`: Počítá průměrnou barvu z okolních bloků (blend radius).
- `get...Color`: Získá základní barvu z biomu a colormapy.
- `getRedstoneColor`: Počítá barvu redstonu podle síly signálu.