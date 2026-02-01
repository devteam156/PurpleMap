# SqliteCommandSet.java

## Přehled

`SqliteCommandSet` je implementace `CommandSet` specifická pro SQLite databáze.

## Umístění

`de.bluecolored.bluemap.core.storage.sql.commandset.SqliteCommandSet`

## Dědičnost

`AbstractCommandSet` -> `SqliteCommandSet`

## SQL Dialekt

Používá specifickou syntaxi SQLite, například:

- `REPLACE INTO` pro zápis dat.
- `AUTOINCREMENT` pro generování ID.
- `sqlite_master` pro kontrolu existujících tabulek.
- `STRICT` režim pro tabulky (vyžaduje novější SQLite).
