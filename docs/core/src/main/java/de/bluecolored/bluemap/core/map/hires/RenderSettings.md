# RenderSettings.java

## Přehled

`RenderSettings` je rozhraní definující nastavení, která ovlivňují proces renderování detailních (high-res) modelů.

## Umístění

`de.bluecolored.bluemap.core.map.hires.RenderSettings`

## Metody (Vlastnosti)

### `getRemoveCavesBelowY()`

Y-úroveň, pod kterou se mají odstraňovat jeskyně (culling). Pokud je nad blokem vzduch a blok je pod touto úrovní, může
být považován za "jeskynní" a nebude vykreslen.

### `getCaveDetectionOceanFloor()`

Alternativní metoda detekce jeskyní relativně k výšce dna oceánu.

### `isCaveDetectionUsesBlockLight()`

Pokud je `true`, používá se pro detekci jeskyní také úroveň blokového světla (nejen skylight).

### `getAmbientLight()`

Výchozí hodnota ambientního světla (0-1).

### `isRenderEdges()`

Zda se mají renderovat "okraje" (stěny) na hranicích mapy, jako by tam končil svět.

### `getEdgeLightStrength()`

Intenzita světla na okrajích mapy.

### `isIgnoreMissingLightData()`

Zda renderovat i chunky, kterým chybí data o osvětlení.

### `getRenderMask()`

Vrací masku (`Mask`), která definuje hranice renderované oblasti.

### `isInsideRenderBoundaries(...)`

Pomocné metody pro kontrolu, zda je daná souřadnice nebo dlaždice uvnitř masky.

### `isSaveHiresLayer()`

Zda se mají vyrenderované high-res dlaždice ukládat.

### `isRenderTopOnly()`

Pokud je `true`, renderuje se pouze "top-down" pohled (optimalizace).
