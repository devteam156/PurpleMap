# File Tree Tools

## Přehled

Sada tříd pro pokročilé a bezpečné operace nad stromovými strukturami souborového systému.

## Umístění

`de.bluecolored.bluemap.core.util`

## Třídy

### `SizeCollectingPathVisitor`

- **Dědičnost:** `SimpleFileVisitor<Path>`
- **Logika:** Prochází soubory a sčítá jejich velikosti v bajtech do `AtomicLong`. Používá se pro zjištění celkové
  velikosti mapy na disku.

### `CopyingPathVisitor`

- **Logika:** Rekurzivně kopíruje soubory a složky z jednoho místa na druhé. Používá se při extrakci webové aplikace
  nebo kopírování resources.

### `DeletingPathVisitor`

- **Logika:** Bezpečně smaže celý podstrom souborů (včetně neprázdných složek).

### `FileTreeWalker` & `FileTreeIterator`

- **Logika:** Vlastní implementace procházení souborů, která je navržena tak, aby byla odolná proti změnám na disku
  během procházení. Pokud soubor zmizí mezi okamžikem, kdy byl nalezen, a okamžikem, kdy má být zpracován, tyto třídy
  chybu potlačí a pokračují dál. To je nezbytné pro asynchronní promazávání cache.

---

# Ostatní Utility

### `Preconditions.java`

- Jednoduché kontroly argumentů (podobně jako v Guava). Vyhazuje `IllegalArgumentException`, pokud podmínka neplatí.

### `IntComparator.java` (Rozhraní)

- Funkcionální rozhraní pro porovnávání dvou primitivních integerů. Snižuje potřebu boxování (Integer vs int).

### `BiIntConsumer.java` (Rozhraní)

- Funkcionální rozhraní pro operace se dvěma integery (např. souřadnice X, Z).

### `Direction.java` (Enum)

- Reprezentuje 6 základních směrů (NORTH, SOUTH, WEST, EAST, UP, DOWN).
- Obsahuje metody pro rotaci, získání opačného směru a převod na vektory.
- Používá se při renderování bloků pro výpočet sousedství a culling.
