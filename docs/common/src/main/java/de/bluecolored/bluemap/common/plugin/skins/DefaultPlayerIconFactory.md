# DefaultPlayerIconFactory.java

## Přehled

`DefaultPlayerIconFactory` je výchozí implementace rozhraní `PlayerIconFactory`. Zajišťuje vytváření ikony hráče (hlavy)
z jeho skinu.

## Umístění

`de.bluecolored.bluemap.common.plugin.skins.DefaultPlayerIconFactory`

## Funkcionalita

Metoda `apply` vezme stažený skin hráče a vyřízne z něj hlavu.

1. Získá první vrstvu hlavy (8x8 pixelů, souřadnice 8,8).
2. Získá druhou vrstvu hlavy (8x8 pixelů, souřadnice 40,8 - "helma/čepice").
3. Vytvoří nový obrázek (48x48 pixelů).
4. Vykreslí první vrstvu zvětšenou na 40x40 pixelů.
5. Vykreslí druhou vrstvu (overlay) zvětšenou na 48x48 pixelů přes první vrstvu.
6. Používá interpolaci `NEAREST_NEIGHBOR` pro zachování pixel-art vzhledu.

## Ošetření chyb

Obsahuje ošetření pro případ, že server běží v "headless" módu a chybí grafické knihovny (`Graphics2D`). V takovém
případě se pokusí vrátit alespoň základní vrstvu hlavy bez zvětšení a overlaye.
