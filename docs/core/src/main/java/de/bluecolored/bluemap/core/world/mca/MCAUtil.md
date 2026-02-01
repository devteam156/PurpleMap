# MCAUtil.java

## Přehled

`MCAUtil` je pomocná třída obsahující nástroje a konfiguraci pro práci s MCA soubory a NBT daty.

## Umístění

`de.bluecolored.bluemap.core.world.mca.MCAUtil`

## Funkcionalita

- **BlueNBT Konfigurace:** Poskytuje nakonfigurovanou instanci `BlueNBT` (`BLUENBT`) se zaregistrovanými deserializéry
  pro specifické typy BlueMap (vektory, UUID, blokové stavy).
- **Bitové operace:** Obsahuje metody pro práci s bitovými proudy (používané při čtení zabalených dat v chuncích).

## Metody

### `addCommonNbtSettings(BlueNBT nbt)`

Přidá standardní deserializéry a nastavení do instance BlueNBT.

### `getValueFromLongStream(...)`

Získá hodnotu z pole longů, které je chápáno jako souvislý proud bitů. Podporuje čtení hodnot, které přetékají hranice
longu.

### `getByteHalf(...)`

Získá horní nebo dolní 4 bity z bytu (pro čtení starších formátů osvětlení).