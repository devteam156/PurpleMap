# Key.java & Keyed.java

## Přehled

`Key` je základní datový typ v BlueMap používaný pro jednoznačnou identifikaci objektů (bloků, biomů, dimenzí). Je
inspirován systémem jmenných prostorů (namespaces) v Minecraftu. Skládá se z `namespace` a `value`.

## Umístění

`de.bluecolored.bluemap.core.util.Key`

## Konstanty

- `MINECRAFT_NAMESPACE`: "minecraft"
- `BLUEMAP_NAMESPACE`: "bluemap"

## Atributy

- `namespace`: `String` - Jmenný prostor (např. "minecraft").
- `value`: `String` - Samotná hodnota (např. "stone").
- `formatted`: `String` - Zformátovaný řetězec `namespace:value`.

## Funkcionalita a Logika

- **Interning:** Všechny řetězce jsou při vytvoření "internovány" (`String.intern()`). To znamená, že identické klíče
  sdílejí stejné instance řetězců v paměti, což umožňuje extrémně rychlé porovnávání pomocí operátoru `==` místo
  `.equals()`.
- **Parsování:** Pokud je konstruktoru předán řetězec bez dvojtečky, automaticky se předpokládá jmenný prostor
  `minecraft`.

## Metody

### `getFormatted()`

Vrátí klíč jako řetězec `namespace:value`.

### `parse(String formatted)`

Statická metoda pro vytvoření klíče z řetězce.

### `minecraft(String value)` / `bluemap(String value)`

Zkratky pro vytvoření klíčů v nejčastějších jmenných prostorech.

---

# Keyed.java (Rozhraní)

Jednoduché rozhraní pro objekty, které mají svůj unikátní `Key`.

- Metoda `getKey()`: Vrátí klíč objektu.
