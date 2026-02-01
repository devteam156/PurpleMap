# PackedIntArrayAccess.java

## Přehled

`PackedIntArrayAccess` je pomocná třída pro přístup k hodnotám v poli `long[]`, které jsou zabaleny (bit-packed) tak, že
jedna hodnota zabírá specifický počet bitů. Tento formát se používá v Minecraftu pro ukládání dat bloků a biomů v
chuncích (od verze 1.13+).

## Umístění

`de.bluecolored.bluemap.core.world.mca.PackedIntArrayAccess`

## Funkcionalita

- Umožňuje čtení celočíselných hodnot (ID) ze zabaleného pole longů.
- Automaticky počítá offsety a masky pro získání správných bitů.
- Používá "magické konstanty" pro rychlé dělení (optimalizace výkonu).

## Konstruktory

- `PackedIntArrayAccess(long[] data, int elementCount)`: Vypočítá počet bitů na element z délky dat a počtu prvků.
- `PackedIntArrayAccess(int bitsPerElement, long[] data)`: Přímá inicializace s počtem bitů na element.

## Metody

### `get(int i)`

Vrátí hodnotu na indexu `i`.

### `isCorrectSize(int expectedSize)`

Ověří, zda kapacita pole odpovídá očekávané velikosti.