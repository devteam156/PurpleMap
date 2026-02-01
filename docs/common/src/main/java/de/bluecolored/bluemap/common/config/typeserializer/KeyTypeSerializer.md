# KeyTypeSerializer.java

## Přehled

Serializátor pro typ `Key` (interní BlueMap identifikátor složený z namespace a hodnoty).

## Umístění

`de.bluecolored.bluemap.common.config.typeserializer.KeyTypeSerializer`

## Formát v konfiguraci

Reprezentován jako jednoduchý řetězec ve formátu `namespace:hodnota`.

## Logika

- **Deserializace:** Přečte string a předá ho konstruktoru `new Key(string)`.
- **Serializace:** Zapíše zformátovaný řetězec z `key.getFormatted()`.