# CombinedMaskSerializer.java

## Přehled

Jeden z nejsložitějších serializátorů. Umožňuje definovat seznam různých typů masek v konfiguraci jedné mapy.

## Umístění

`de.bluecolored.bluemap.common.config.typeserializer.CombinedMaskSerializer`

## Formát v konfiguraci

Maska je v konfiguraci seznamem objektů. Každý objekt musí mít pole `type`.

```hocon
render-mask: [
  {
    type: box
    min-x: 0, ...
  },
  {
    type: circle
    subtract: true, ...
  }
]
```

## Logika Deserializace

1. Vytvoří novou prázdnou `CombinedMask`.
2. Prochází všechny uzly v seznamu:
    - Nejdříve načte uzel jako `MaskConfig.Base` (aby získal informaci o typu).
    - Zjistí konkrétní třídu konfigurace pro daný typ (např. `BoxMaskConfig.class`).
    - Znovu načte uzel s touto konkrétní třídou.
    - Zavolá `maskConfig.addTo(combinedMask)`, což vytvoří geometrickou masku a přidá ji do výsledku.
3. Vrátí naplněnou složenou masku.

## Logika Serializace

Není implementována (vypisování masek do configu z kódu není potřeba).