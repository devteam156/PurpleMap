# Vector2iTypeSerializer.java

## Přehled

`Vector2iTypeSerializer` je implementace `TypeSerializer` z knihovny Configurate pro serializaci a deserializaci objektů
`Vector2i` (dvojice celých čísel).

## Umístění

`de.bluecolored.bluemap.common.config.typeserializer.Vector2iTypeSerializer`

## Implementovaná Rozhraní

`TypeSerializer<Vector2i>`

## Funkcionalita

### `deserialize(...)`

Načte `Vector2i` z konfiguračního uzlu.

- Očekává objekt s klíči `x` a `y`.
- Podporuje fallback: pokud chybí `y`, pokusí se načíst hodnotu z klíče `z`.
- Vyhodí `SerializationException`, pokud chybí souřadnice.

### `serialize(...)`

Uloží `Vector2i` do konfiguračního uzlu jako objekt s klíči `x` a `y`.
