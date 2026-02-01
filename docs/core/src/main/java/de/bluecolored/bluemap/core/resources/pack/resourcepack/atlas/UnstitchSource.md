# UnstitchSource.java

## Přehled

`UnstitchSource` je typ zdroje v atlasu, který vezme existující texturu a "rozstříhá" ji na menší části (regions).
Původní textura se zahodí. Toto se používá například pro rozdělení textur `painting.png` na jednotlivé obrazy.

## Umístění

`de.bluecolored.bluemap.core.resources.pack.resourcepack.atlas.UnstitchSource`

## Dědičnost

`Source` -> `UnstitchSource`

## Atributy (z JSONu)

- `resource`: Cesta k zdrojové textuře.
- `divisor_x`, `divisor_y`: Dělitel rozměrů. Pokud není zadán, použije se velikost obrázku (což znamená, že souřadnice
  regionů jsou v pixelech).
- `regions`: Seznam oblastí, které se mají vystřihnout.

## Metody

### `load(...)`

Načte zdrojovou texturu do poolu.

### `bake(...)`

Provede rozstříhání.

1. Načte zdrojovou texturu.
2. Pro každý region:
    - Vypočítá souřadnice v pixelech (s ohledem na divisory).
    - Vytvoří pod-obrázek (`getSubimage`).
    - Uloží novou texturu pod názvem definovaným v regionu (`sprite`).
    - Zkontroluje `textureFilter`, zda je textura potřeba.
