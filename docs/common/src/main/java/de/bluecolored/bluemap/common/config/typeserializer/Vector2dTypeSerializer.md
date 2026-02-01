# Vector2dTypeSerializer.java

## Přehled

`Vector2dTypeSerializer` je implementace `TypeSerializer` z knihovny Configurate pro serializaci a deserializaci objektů
`Vector2d` (dvojice reálných čísel).

## Umístění

`de.bluecolored.bluemap.common.config.typeserializer.Vector2dTypeSerializer`

## Implementovaná Rozhraní

`TypeSerializer<Vector2d>`

## Funkcionalita

### `deserialize(...)`

Načte `Vector2d` z konfiguračního uzlu.

- Očekává objekt s klíči `x` a `y`.
- Podporuje fallback: pokud chybí `y`, pokusí se načíst hodnotu z klíče `z` (užitečné pro konverzi 2D souřadnic, které
  reprezentují XZ rovinu v Minecraftu).
- Vyhodí `SerializationException`, pokud chybí souřadnice.

### `serialize(...)`

Uloží `Vector2d` do konfiguračního uzlu jako objekt s klíči `x` a `y`.
