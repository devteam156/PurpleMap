# BannerBlockEntity.java

## Přehled

Uchovává data o vlajkách (banners), zejména jejich barevné vzory.

## Umístění

`de.bluecolored.bluemap.core.world.mca.blockentity.BannerBlockEntity`

## Atributy

- `customName`: Vlastní název vlajky.
- `patterns`: Seznam aplikovaných vzorů (`Pattern`).

## Vnořené třídy

### `Pattern`

- `pattern`: Kód vzoru (např. "bs" pro pruh).
- `color`: Barva vzoru.
- (Aktuálně implementováno jako `Object`, protože BlueMap plně nevyužívá vnitřní detaily vzorů při renderování 3D mapy,
  ale zachovává data pro budoucí použití).