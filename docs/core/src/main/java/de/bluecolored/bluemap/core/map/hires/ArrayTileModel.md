# ArrayTileModel.java

## Přehled

`ArrayTileModel` je implementace `TileModel`, která ukládá geometrii (vrcholy, UV souřadnice, barvy atd.) do
primitivních polí (`float[]`, `int[]`, `byte[]`). Je navržena pro vysoký výkon a minimální alokaci objektů.

## Umístění

`de.bluecolored.bluemap.core.map.hires.ArrayTileModel`

## Vlastnosti

- **Pooling:** Instance `ArrayTileModel` jsou recyklovány pomocí `InstancePool`, aby se snížil tlak na Garbage
  Collector (GC).
- **Atributy:** Ukládá pozice, UV, AO (ambient occlusion), barvu, světlo (sluneční, blokové) a index materiálu (
  textury).
- **Kapacita:** Dynamicky se zvětšuje podle potřeby. Pokud je příliš velká, po čase se zmenší.

## Metody

Poskytuje nízkoúrovňové metody pro nastavování atributů jednotlivých vrcholů trojúhelníků (face).

- `add(int count)`: Rezervuje místo pro další trojúhelníky.
- `setPositions(...)`: Nastaví souřadnice vrcholů.
- `setUvs(...)`, `setAOs(...)`, `setColor(...)`: Nastaví další atributy.
- `rotate(...)`, `scale(...)`, `translate(...)`, `transform(...)`: Provádí transformace modelu.
- `sort()`: Seřadí trojúhelníky podle indexu materiálu (textury). To je důležité pro efektivní renderování a kompresi.

### `instancePool()`

Statická metoda pro získání poolu instancí.
