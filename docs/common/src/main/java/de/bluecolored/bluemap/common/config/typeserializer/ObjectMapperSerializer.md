# ObjectMapperSerializer.java

## Přehled

Univerzální serializátor, který deleguje práci na standardní `ObjectMapper` knihovny Configurate. Používá se pro
polymorfní typy jako `StorageConfig` nebo `MaskConfig`.

## Umístění

`de.bluecolored.bluemap.common.config.typeserializer.ObjectMapperSerializer`

## Logika

Pouze získá továrnu pro daný typ a zavolá `load` (pro deserializaci) nebo `save` (pro serializaci). Slouží jako lepidlo
pro registraci typů, které nemají přímo anotaci `@ConfigSerializable`, ale chceme je tak zpracovávat.