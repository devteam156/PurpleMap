# BlockEntityType.java

## Přehled

Registr typů blokových entit. Slouží k určení, která Java třída se má použít pro deserializaci konkrétního NBT tagu.

## Umístění

`de.bluecolored.bluemap.core.world.mca.blockentity.BlockEntityType`

## Registrované Typy

- `SIGN`: `SignBlockEntity` (pro normální cedulky).
- `HANGING_SIGN`: Také `SignBlockEntity` (pro visací cedulky).
- `SKULL`: `SkullBlockEntity`.
- `BANNER`: `BannerBlockEntity`.

## Metody

- `getBlockEntityClass()`: Vrátí třídu (např. `SkullBlockEntity.class`), která má být vytvořena pro daný typ z registru.