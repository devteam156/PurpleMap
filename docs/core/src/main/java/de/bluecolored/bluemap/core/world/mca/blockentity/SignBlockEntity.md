# SignBlockEntity.java

## Přehled

Třída pro zpracování dat cedulek. Podporuje jak moderní formát (1.20+ s textem na obou stranách), tak starší (legacy)
formát.

## Umístění

`de.bluecolored.bluemap.core.world.mca.blockentity.SignBlockEntity`

## Dědičnost

`MCABlockEntity` -> `SignBlockEntity`

## Atributy (Moderní formát)

- `frontText`: `TextData` - Text na přední straně.
- `backText`: `TextData` - Text na zadní straně.

## Vnořené třídy

### `TextData`

- `hasGlowingText`: Zda text svítí (použití inkoustu z chobotnice).
- `color`: Barva textu (výchozí "black").
- `messages`: Seznam 4 řádků textu (uloženo jako JSON objekty/stringy).

### `LegacySignBlockEntity`

Specializace pro verze před 1.20.

- Přepisuje `getFrontText()` tak, aby mapoval stará NBT pole (`Text1`, `Text2`...) na moderní strukturu `TextData`. To
  umožňuje zbytku BlueMap pracovat s cedulkami jednotně bez ohledu na verzi světa.