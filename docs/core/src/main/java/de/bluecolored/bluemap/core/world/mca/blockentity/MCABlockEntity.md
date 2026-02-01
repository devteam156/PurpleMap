# MCABlockEntity.java (Základní třída)

## Přehled

`MCABlockEntity` je základní implementace rozhraní `BlockEntity` pro formát MCA. Obsahuje společná data, která má každá
bloková entita v Minecraftu uložená v NBT.

## Umístění

`de.bluecolored.bluemap.core.world.mca.blockentity.MCABlockEntity`

## Atributy

- `id`: `Key` - Identifikátor typu entity (např. `minecraft:sign`).
- `x`, `y`, `z`: `int` - Absolutní souřadnice bloku ve světě.
- `keepPacked`: `boolean` - Interní příznak z NBT (používaný Minecraftem při přesunu dat).

## Použití

Slouží jako základ pro specializované entity. Pokud BlueMap narazí na neznámý typ entity, použije tuto základní třídu,
aby znal alespoň pozici a ID.