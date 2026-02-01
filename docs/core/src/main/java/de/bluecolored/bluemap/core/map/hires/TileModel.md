# TileModel.java

## Přehled

`TileModel` je rozhraní pro 3D model jedné mapové dlaždice. Model se skládá z trojúhelníků (triangles/faces). Každý
vrchol (vertex) má sadu atributů.

## Umístění

`de.bluecolored.bluemap.core.map.hires.TileModel`

## Atributy

- **Positions**: XYZ souřadnice (3x float).
- **UVs**: Texturovací souřadnice (2x float).
- **AOs**: Ambient occlusion hodnoty (1x float/byte).
- **Color**: RGB barva (3x float).
- **Sunlight, Blocklight**: Úrovně světla (int/byte).
- **MaterialIndex**: ID materiálu/textury (int).

## Metody

Většina metod slouží k zápisu dat do modelu.

- `size()`: Vrací počet trojúhelníků v modelu.
- `add(int count)`: Přidá (rezervuje) místo pro `count` trojúhelníků.
- `setPositions(...)`, `setUvs(...)`, `setAOs(...)`, `setColor(...)` ...: Nastaví atributy pro konkrétní trojúhelník (
  `face` index).
- `transform(...)`, `rotate(...)`, `scale(...)`, `translate(...)`: Aplikuje transformace na rozsah trojúhelníků.
- `invertOrientation(int face)`: Obrátí orientaci trojúhelníku (prohodí pořadí vrcholů a UV).
- `sort()`: Seřadí trojúhelníky (typicky podle materiálu).
- `reset(int size)`: Zmenší model na danou velikost.
- `clear()`: Vymaže model.
