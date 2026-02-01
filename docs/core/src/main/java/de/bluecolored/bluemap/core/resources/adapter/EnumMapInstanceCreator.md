# EnumMapInstanceCreator.java

## Přehled

`EnumMapInstanceCreator` je pomocná třída pro GSON, která umožňuje vytvářet instance `EnumMap` s konkrétním typem
klíče (Enum).

## Umístění

`de.bluecolored.bluemap.core.resources.adapter.EnumMapInstanceCreator`

## Implementovaná Rozhraní

`InstanceCreator<EnumMap<K, V>>`

## Metody

### `createInstance(Type type)`

Vytvoří novou, prázdnou instanci `EnumMap` pro definovaný typ Enumu. GSON to potřebuje, protože `EnumMap` nemá
bezparametrický konstruktor (vyžaduje typ klíče v konstruktoru).
