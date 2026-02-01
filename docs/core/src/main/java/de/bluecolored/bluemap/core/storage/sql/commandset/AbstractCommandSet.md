# AbstractCommandSet.java

## Přehled

`AbstractCommandSet` je abstraktní základ pro implementace `CommandSet` pro různé SQL dialekty (MySQL, PostgreSQL,
SQLite). Obsahuje společnou logiku pro práci s databází, cachování klíčů a přípravu SQL dotazů.

## Umístění

`de.bluecolored.bluemap.core.storage.sql.commandset.AbstractCommandSet`

## Implementovaná Rozhraní

`CommandSet`

## Funkcionalita

- **Inicializace tabulek:** Kontroluje existenci tabulek a vytváří je, pokud chybí.
- **Normalizace klíčů:** Pro mapy, komprese, typy úložišť atd. používá číselná ID (foreign keys) místo opakování
  textových řetězců. Tyto ID cachuje (`LoadingCache`).
- **CRUD operace:** Implementuje metody pro čtení, zápis a mazání dat pomocí abstraktních metod, které vracejí konkrétní
  SQL dotazy.

## Abstraktní metody (SQL Statementy)

Podtřídy musí implementovat metody vracející SQL dotazy pro konkrétní dialekt:

- `create...TableStatement()`
- `...WriteStatement()`
- `...ReadStatement()`
- `...DeleteStatement()`
- atd.
