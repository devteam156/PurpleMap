# SkullBlockEntity.java

## Přehled

Reprezentuje blok lebe (hlavy). Nejdůležitější částí je profil hráče, který BlueMap používá k získání textury skinu pro
danou hlavu.

## Umístění

`de.bluecolored.bluemap.core.world.mca.blockentity.SkullBlockEntity`

## Dědičnost

`MCABlockEntity` -> `SkullBlockEntity`

## Atributy

- `customName`: Vlastní jméno hlavy.
- `noteBlockSound`: Zvuk, který hlava vydává na note blocku (od 1.20+).
- `profile`: `Profile` - Objekt obsahující data o hráči.

## Vnořené třídy

### `Profile`

- `id`: UUID hráče.
- `name`: Jméno hráče.
- `properties`: Seznam vlastností (obsahuje Base64 zakódovaná data o skinu).

### `Property`

- `name`: Název (obvykle "textures").
- `value`: Samotná Base64 data skinu.
- `signature`: Digitální podpis dat (ověřuje pravost skinu).