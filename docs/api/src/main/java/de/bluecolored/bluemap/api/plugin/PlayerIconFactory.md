# PlayerIconFactory.java

## Přehled

`PlayerIconFactory` je funkcionální rozhraní, které rozšiřuje `BiFunction<UUID, BufferedImage, BufferedImage>`. Slouží k
vytváření ikon (obrázků) pro markery hráčů na mapě na základě jejich UUID a staženého skinu.

## Umístění

`de.bluecolored.bluemap.api.plugin.PlayerIconFactory`

## Metody

### `apply(UUID playerUuid, BufferedImage playerSkin)`

**Popis:**
Tato metoda přijme UUID hráče a jeho skin (jako `BufferedImage`) a vygeneruje novou ikonu.

**Parametry:**

- `playerUuid` (`UUID`): Unikátní identifikátor hráče.
- `playerSkin` (`BufferedImage`): Vstupní obrázek skinu hráče.

**Návratová hodnota:**

- `BufferedImage`: Nově vygenerovaný obrázek, který bude použit jako ikona hráče na mapě.

**Poznámka:**
Metoda by měla vždy vracet **novou** instanci `BufferedImage` a nemodifikovat vstupní `playerSkin`, pokud to není záměr.

## Použití

Používá se v rámci `Plugin` rozhraní (`getPlayerMarkerIconFactory` / `setPlayerMarkerIconFactory`). Umožňuje přizpůsobit
vzhled ikon hráčů – například oříznout pouze hlavu, přidat overlay, rámeček, nebo změnit velikost.
