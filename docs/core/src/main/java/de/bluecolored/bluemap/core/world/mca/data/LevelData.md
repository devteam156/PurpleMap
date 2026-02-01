# LevelData.java

## Přehled

`LevelData` je datová třída reprezentující obsah souboru `level.dat`. Tento soubor obsahuje globální informace o světě.

## Umístění

`de.bluecolored.bluemap.core.world.mca.data.LevelData`

## Atributy (z NBT)

- `levelName`: Jméno levelu.
- `spawn`: Souřadnice spawnu.
- `worldGenSettings`: Nastavení generování světa, včetně definic dimenzí.

## Vnořené třídy

- `Data`: Obaluje samotná data.
- `Spawn`: Reprezentuje bod spawnu (dimenze, pozice, rotace).
- `WGSettings`: Obsahuje mapu dimenzí.
- `Dimension`: Obsahuje typ dimenze (`DimensionType`).

## Funkcionalita

- Poskytuje přístup k informacím o spawnu a dimenzích světa.
- Podporuje starší formát uložení spawnu (přímo v kořeni `Data` jako `SpawnX`, `SpawnY`, `SpawnZ`), který transparentně
  převádí na objekt `Spawn`.
