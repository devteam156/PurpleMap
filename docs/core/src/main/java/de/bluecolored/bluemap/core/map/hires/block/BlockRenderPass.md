# BlockRenderPass.java

## Přehled

`BlockRenderPass` je implementace `RenderPass` určená pro vykreslování bloků (terénu) do modelu dlaždice.

## Umístění

`de.bluecolored.bluemap.core.map.hires.block.BlockRenderPass`

## Funkcionalita

1. Prochází všechny bloky v dané oblasti (definované `modelMin` a `modelMax`).
2. Pro každý sloupec bloků (X, Z) hledá nejvyšší viditelný blok (`maxHeight`) a počítá barvu sloupce pro low-res mapu.
3. Pro každý blok volá `BlockStateModelRenderer` k vygenerování geometrie.
4. Spravuje:
    - **Render boundaries**: Ignoruje bloky mimo renderovanou oblast.
    - **Top-only render**: Optimalizace, kdy se renderuje pouze povrch.
    - **Low-res data**: Zapisuje vypočítanou barvu, výšku a světlo do `tileMetaConsumer`.

## Metody

### `render(...)`

Hlavní smyčka přes souřadnice X, Z a Y.
