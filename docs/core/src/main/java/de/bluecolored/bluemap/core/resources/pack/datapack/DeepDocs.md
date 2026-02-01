# DataPack System

## Přehled

Balíček `de.bluecolored.bluemap.core.resources.pack.datapack` spravuje logická data Minecraftu, která nejsou vizuální (
modely), ale definují chování světa (biomy, dimenze). BlueMap tato data čte ze standardních Minecraft JSON souborů v
adresářích `data/`.

---

# DataPack.java (Hlavní třída)

## Přehled

Spravuje pooly pro `DimensionType` a `Biome`. Zajišťuje načítání konfigurací světů.

## Vnitřní Logika: Načítání a prioritizace

- **`loadPath`**: Prochází adresář `data/minecraft/worldgen/biome` a `data/minecraft/dimension_type`.
- **`bake()`**:
    - Pokud v načtených datech chybí definice pro standardní dimenze (Overworld, Nether, End), BlueMap automaticky
      dosadí své vestavěné verze.
    - Inicializuje `LegacyBiomes`, což je systém pro zpětnou kompatibilitu se starými světy, které nepoužívají jmenné
      prostory pro biomy, ale číselná ID.

---

# DatapackBiome.java

## Přehled

Implementace rozhraní `Biome`, která přímo mapuje vlastnosti z Minecraft JSON souborů biomů.

## Vnitřní Logika a Data

- **Struktura JSONu:** Kopíruje hierarchii Minecraftu (`effects`, `temperature`, `downfall`).
- **`waterColor`**: BlueMap v metodě `init()` automaticky vynucuje Alfu 1.0 pro barvu vody, aby se zamezilo chybám při
  renderování (voda v BlueMap je řešena jiným algoritmem průhlednosti).
- **`grassColorModifier`**: Pokud je v JSONu zadán speciální modifikátor (např. `swamp`), BlueMap ho automaticky vyhledá
  ve svém registru a aplikuje při výpočtu barev.

---

# DimensionTypeData.java

## Přehled

Implementace rozhraní `DimensionType`. Tato data BlueMap získává buď ze souborů regionů (`level.dat`), nebo z DataPacků.

## Klíčová Data

- **`min_y` & `height`**: Definují vertikální rozsah světa. Renderer tyto hodnoty používá k určení, kde začít a skončit
  renderování sloupců.
- **`ambient_light`**: Ovlivňuje základní úroveň jasu bloků v místech bez přímého světla (např. v Netheru).
- **`has_skylight`**: Určuje, zda má renderer počítat se slunečním světlem.
- **`has_ceiling`**: Pokud je true, BlueMap ví, že dimenze má strop (Nether), a renderer může aktivovat specifické
  optimalizace nebo ořezy.
