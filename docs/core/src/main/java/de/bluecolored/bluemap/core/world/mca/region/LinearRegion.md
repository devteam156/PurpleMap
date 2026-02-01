# LinearRegion.java

## Přehled

`LinearRegion` je implementace rozhraní `Region` pro formát **Linear**. Linear je alternativní formát regionů (vyvíjený
pro optimalizaci výkonu a komprese), který používají některé modované servery nebo pluginy.

## Umístění

`de.bluecolored.bluemap.core.world.mca.region.LinearRegion`

## Formát

- Používá soubory s příponou `.linear`.
- Všechny chunky jsou komprimovány dohromady pomocí ZSTD.
- Obsahuje hlavičku s časovými razítky a offsety.

## Funkcionalita

- Načte hlavičku souboru.
- Dekomprimuje celý blok dat (ZSTD).
- Umožňuje iterovat přes chunky a načítat je.
