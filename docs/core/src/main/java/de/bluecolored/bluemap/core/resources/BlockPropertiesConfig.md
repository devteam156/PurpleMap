# BlockPropertiesConfig.java

## Přehled

Načítá a poskytuje konfiguraci vlastností bloků (např. `occluding`, `culling`, `alwaysWaterlogged`) ze souborů
`blockProperties.json`.

## Umístění

`de.bluecolored.bluemap.core.resources.BlockPropertiesConfig`

## Funkcionalita

- **Načítání (`load`):** Parsuje JSON, kde klíčem je řetězec bloku (např. `minecraft:grass_block[snowy=true]`) a
  hodnotou objekt s vlastnostmi.
- **Získání vlastností (`getBlockProperties`):** Projde načtená mapování a vrátí vlastnosti pro první mapování, které
  odpovídá danému bloku. Pokud žádné neodpovídá, vrátí `BlockProperties.DEFAULT`.