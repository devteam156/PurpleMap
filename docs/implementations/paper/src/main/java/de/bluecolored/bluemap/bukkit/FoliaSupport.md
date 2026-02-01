# FoliaSupport.java

## Přehled

`FoliaSupport` je pomocná třída pro detekci prostředí Folia (multithreaded fork Paperu).

## Umístění

`de.bluecolored.bluemap.bukkit.FoliaSupport`

## Funkcionalita

- **Detekce:** Zjišťuje přítomnost Folia pomocí kontroly existence třídy
  `io.papermc.paper.threadedregions.RegionizedServer`.
- **Statická konstanta:** `IS_FOLIA` (boolean) indikuje, zda server běží na Folia.

## Použití

Tato třída umožňuje ostatním částem pluginu přizpůsobit své chování specifikám Folia (např. jinak plánovat úlohy nebo
přistupovat k regionům).
