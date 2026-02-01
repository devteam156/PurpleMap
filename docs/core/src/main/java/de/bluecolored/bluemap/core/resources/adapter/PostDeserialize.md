# PostDeserialize.java

## Přehled

`@PostDeserialize` je anotace, kterou lze umístit na metodu (bez parametrů) v třídě. Tato metoda bude automaticky
zavolána ihned po deserializaci objektu z JSONu pomocí GSONu (pokud je zaregistrován `PostDeserializeAdapterFactory`).

## Umístění

`de.bluecolored.bluemap.core.resources.adapter.PostDeserialize`

## Použití

Užitečné pro:

- Validaci načtených dat.
- Inicializaci polí, která nebyla v JSONu (např. transient pole).
- Přepočet odvozených hodnot.
