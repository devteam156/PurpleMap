# LowresLayer.java

## Přehled

`LowresLayer` reprezentuje jednu vrstvu LOD (Level of Detail) v pyramidě dlaždic pro low-res mapu. Stará se o načítání,
ukládání a aktualizaci `LowresTile` (dlaždic) v této vrstvě a o propagaci změn do vyšší (méně detailní) vrstvy.

## Umístění

`de.bluecolored.bluemap.core.map.lowres.LowresLayer`

## Atributy

- `storage`: Úložiště pro čtení/zápis dlaždic.
- `tileGrid`: Mřížka definující rozložení dlaždic v této vrstvě.
- `lodFactor`: Faktor zmenšení pro další vrstvu (např. 5 znamená, že 5x5 pixelů této vrstvy se průměruje do 1 pixelu
  další vrstvy).
- `lod`: Číslo LOD (0 je nejdetailnější lowres, vyšší čísla jsou méně detailní).
- `nextLayer`: Odkaz na další (vyšší) vrstvu LOD. Může být `null`, pokud je toto nejvyšší vrstva.
- `pendingChanges`: Mapa dlaždic, které byly změněny a čekají na uložení.

## Metody

### `save()`

Uloží všechny čekající změny na disk.

- Pro každou změněnou dlaždici zavolá `saveTile`.
- Pokud se uloží příliš mnoho změn, které nejdou zapsat, zahodí je (`DISCARD_THRESHOLD`), aby nedošlo k OOM.

### `discard()`

Zahodí všechny neuložené změny a vyčistí cache.

### `saveTile(Vector2i tilePos, LowresTile tile)`

Uloží jednu dlaždici.

1. Zapíše dlaždici do `storage`.
2. Pokud existuje `nextLayer`, vypočítá průměrnou barvu, výšku a světlo pro skupinu pixelů (podle `lodFactor`) a pošle
   tato data do další vrstvy (`nextLayer.set`). Tím se změny propagují rekurzivně až do nejvyššího LOD.

### `set(int cellX, int cellZ, int pixelX, int pixelZ, Color color, int height, int blockLight)`

Nastaví hodnotu pixelu v této vrstvě.

- `cellX`, `cellZ`: Souřadnice dlaždice.
- `pixelX`, `pixelZ`: Souřadnice pixelu v rámci dlaždice.
- Automaticky řeší "seamless edges" (bezešvé okraje) tím, že zapisuje i do sousedních dlaždic, pokud je pixel na okraji.
