# RenderPassType.java

## Přehled

`RenderPassType` je registr a identifikátor typů renderovacích průchodů. Umožňuje definovat a získávat různé typy
průchodů (např. bloky, entity) pomocí klíčů.

## Umístění

`de.bluecolored.bluemap.core.map.hires.RenderPassType`

## Implementovaná Rozhraní

`Keyed`, `RenderPassFactory`

## Konstanty / Registry

- `BLOCKS`: Průchod pro renderování bloků (`BlockRenderPass`).
- `ENTITIES`: Průchod pro renderování entit (`EntityRenderPass`).
- `REGISTRY`: Registr všech dostupných typů.

## Metody

Deleguje metodu `create` na vnitřní `RenderPassFactory`.
