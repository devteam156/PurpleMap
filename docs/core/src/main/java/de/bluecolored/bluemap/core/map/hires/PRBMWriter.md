# PRBMWriter.java

## Přehled

`PRBMWriter` (Poly-Rep-BlueMap Writer) slouží k serializaci (ukládání) objektů `ArrayTileModel` do binárního formátu
`.prbm` (nebo `.json` v závislosti na kontextu, ale zde jde o binární formát používaný prohlížečem). Tento formát je
optimalizován pro rychlé načítání a renderování ve webovém prohlížeči.

## Umístění

`de.bluecolored.bluemap.core.map.hires.PRBMWriter`

## Implementovaná Rozhraní

`Closeable`

## Formát PRBM (Stručně)

Soubor začíná hlavičkou s verzí a informacemi o atributech. Následují pole dat pro jednotlivé atributy vrcholů (vertex
attributes):

- **Position (pozice):** 3x float
- **Normal (normála):** 3x byte (normalizované)
- **Color (barva):** 3x byte (normalizované RGB)
- **UV (texturovací souřadnice):** 2x float
- **AO (ambient occlusion):** 1x byte (normalizované)
- **Blocklight:** 1x byte (nebo 3x byte pro barvu světla?)
- **Sunlight:** 1x byte

Na konci jsou definovány "materiálové skupiny" (Material Groups), které určují, která část geometrie používá jakou
texturu (materiál). To umožňuje efektivní vykreslování s minimem změn stavu (texture bind).

## Metody

### `write(ArrayTileModel model)`

Zapíše celý model do výstupního proudu.

1. Zapíše hlavičku.
2. Zapíše pole atributů (pozice, normály, barvy...). Normály se počítají dynamicky z pozic vrcholů.
3. Zapíše skupiny materiálů (indexy textur).

### `calculateSurfaceNormal(...)`

Pomocná metoda pro výpočet normály trojúhelníku (face) z jeho vrcholů.
