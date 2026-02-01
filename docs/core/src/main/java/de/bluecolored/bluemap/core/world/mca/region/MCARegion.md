# MCARegion.java

## Přehled

`MCARegion` je implementace rozhraní `Region` pro standardní formát **MCA (Anvil)**.

## Umístění

`de.bluecolored.bluemap.core.world.mca.region.MCARegion`

## Formát

- Soubory `.mca`.
- Velikost regionu je 32x32 chunků.
- Obsahuje hlavičku s offsety (lokace chunků v souboru) a časovými razítky.
- Každý chunk je komprimován zvlášť (GZIP nebo Zlib).

## Funkcionalita

- Čte hlavičku regionu.
- Umožňuje načíst konkrétní chunk (`loadChunk`).
- Umožňuje iterovat přes všechny chunky (`iterateAllChunks`) a filtrovat je podle časového razítka.
