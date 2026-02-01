# DebugDump.java

## Přehled

`DebugDump` je anotace, která řídí chování `StateDumper`u při serializaci objektů.

## Umístění

`de.bluecolored.bluemap.common.debug.DebugDump`

## Použití

Může být umístěna na:

- **Typ (Třídu):** Určuje, zda se mají serializovat pole této třídy (defaultně se serializují jen pole tříd v balíčku
  `de.bluecolored.bluemap` nebo třídy s touto anotací).
- **Pole (Field):**
    - `exclude=true`: Pole bude ignorováno.
    - `value="nazev"`: Pole bude v JSONu uvedeno pod jiným názvem.
- **Metodu:** Metoda bude zavolána a její návratová hodnota bude zahrnuta do dumpu.