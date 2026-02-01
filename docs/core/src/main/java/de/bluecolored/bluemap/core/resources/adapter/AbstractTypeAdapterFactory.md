# AbstractTypeAdapterFactory.java

## Přehled

`AbstractTypeAdapterFactory` je pomocná abstraktní třída pro vytváření GSON `TypeAdapterFactory`. Zjednodušuje
registraci adaptérů, které pracují s konkrétním typem třídy.

## Umístění

`de.bluecolored.bluemap.core.resources.adapter.AbstractTypeAdapterFactory`

## Implementovaná Rozhraní

`TypeAdapterFactory`

## Generika

- `<T>`: Typ, pro který tento adaptér slouží.

## Metody

### `create(Gson gson, TypeToken<U> type)`

Implementuje metodu továrny. Zkontroluje, zda požadovaný typ `U` odpovídá typu `T` (nebo je jeho podtřídou). Pokud ano,
vrátí instanci `Adapter` (vnitřní třída), jinak vrátí `null`.

### `read(...)` / `write(...)`

Abstraktní metody, které musí implementovat podtřída. Provádí samotnou serializaci/deserializaci.
