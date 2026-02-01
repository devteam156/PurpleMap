# StateDumper.java

## Přehled

`StateDumper` je nástroj pro diagnostiku a ladění, který umožňuje vyexportovat aktuální stav aplikace (objektů, vláken,
systémových informací) do souboru ve formátu JSON.

## Umístění

`de.bluecolored.bluemap.common.debug.StateDumper`

## Funkcionalita

- **Globální instance:** Udržuje globální instanci `GLOBAL`, do které se mohou registrovat objekty ke sledování.
- **Export (Dump):** Metoda `dump(Path file)` vytvoří JSON soubor obsahující:
    - Systémové informace (verze Javy, OS, paměť, verze BlueMap).
    - Seznam všech běžících vláken a jejich stacktrace.
    - Stav všech registrovaných objektů (`dumpInstance`).
- **Rekurzivní serializace:** Prochází objekty a jejich pole (pomocí reflexe) a serializuje je.
    - Detekuje cykly (aby nedošlo k nekonečné smyčce).
    - Speciální podpora pro kolekce, mapy a pole (vypisuje velikost a prvních několik prvků).
    - Podpora pro Caffeine Cache (statistiky, odhadovaná velikost).
    - Respektuje anotaci `@DebugDump`.

## Metody

### `dump(Path file)`

Hlavní metoda pro vytvoření dumpu.

### `register(Object instance)`

Přidá objekt do seznamu sledovaných instancí.