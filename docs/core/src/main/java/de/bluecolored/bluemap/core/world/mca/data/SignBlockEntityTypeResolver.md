# SignBlockEntityTypeResolver.java

## Přehled

`SignBlockEntityTypeResolver` je `TypeResolver` pro BlueNBT, který rozhoduje, jakou třídu použít pro deserializaci
cedulky (`SignBlockEntity`).

## Umístění

`de.bluecolored.bluemap.core.world.mca.data.SignBlockEntityTypeResolver`

## Funkcionalita

Rozlišuje mezi dvěma formáty cedulek:

1. **Nový formát (1.20+):** Text je uložen v objektech `front_text` a `back_text`. Použije se třída `SignBlockEntity`.
2. **Starý formát (Legacy):** Text je uložen přímo v kořeni entity (`Text1`, `Text2`...). Použije se třída
   `LegacySignBlockEntity`.

Rozhodnutí se provádí na základě přítomnosti pole `front_text`.
