# ExtendedBlock.java

## Přehled

`ExtendedBlock` rozšiřuje základní `BlockAccess` o kontext potřebný pro renderování. Obaluje jiný `BlockAccess` (typicky
`Block`) a přidává přístup k resource packu, nastavení renderování a výpočet vlastností bloku.

## Umístění

`de.bluecolored.bluemap.core.world.block.ExtendedBlock`

## Implementovaná Rozhraní

`BlockAccess`

## Atributy

- `blockAccess`: Podkladový přístup k datům světa.
- `resourcePack`: Zdroj modelů a textur.
- `renderSettings`: Nastavení renderování.
- `properties`: Cachované vlastnosti bloku (`BlockProperties`).
- `renderMask`: Cachovaná maska pro danou oblast.

## Metody

### `getBlockState()`

Vrátí stav bloku. Pokud je zapnuto `isRenderEdges` a blok je mimo hranice renderování, vrátí `AIR` (aby se vytvořila "
stěna" na okraji mapy).

### `getLightData()`

Vrátí data o světle. Upravuje světlo na okrajích mapy (`renderEdges`).

### `getProperties()`

Získá (a cachuje) vlastnosti bloku (culling, occlusion) z `resourcePack`.

### `isInsideRenderBounds()`

Zkontroluje, zda je blok uvnitř renderované oblasti (podle masky).

### `isRemoveIfCave()`

Zkontroluje, zda má být blok odstraněn jako jeskyně (culling podle Y a oceánu).
