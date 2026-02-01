# PostDeserializeAdapterFactory.java

## Přehled

`PostDeserializeAdapterFactory` je továrna pro GSON adaptéry, která zajišťuje volání metod anotovaných
`@PostDeserialize`.

## Umístění

`de.bluecolored.bluemap.core.resources.adapter.PostDeserializeAdapterFactory`

## Implementovaná Rozhraní

`TypeAdapterFactory`

## Funkcionalita

1. Prochází metody třídy, která se má deserializovat.
2. Pokud najde metodu s anotací `@PostDeserialize` (a bez parametrů):
    - Vytvoří nový `TypeAdapter`.
    - Tento adaptér deleguje čtení JSONu na standardní GSON adaptér (`delegate.read(in)`).
    - Po úspěšném načtení objektu zavolá nalezenou metodu pomocí reflexe (`method.invoke(obj)`).
    - Vrátí načtený objekt.
3. Pokud anotaci nenajde, vrátí `null` (GSON použije další dostupný adaptér).
