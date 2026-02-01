# PostgreSQLCommandSet.java

## Přehled

`PostgreSQLCommandSet` je implementace `CommandSet` specifická pro PostgreSQL databáze.

## Umístění

`de.bluecolored.bluemap.core.storage.sql.commandset.PostgreSQLCommandSet`

## Dědičnost

`AbstractCommandSet` -> `PostgreSQLCommandSet`

## SQL Dialekt

Používá specifickou syntaxi PostgreSQL, například:

- `INSERT ... ON CONFLICT DO UPDATE` pro zápis dat (upsert).
- `SERIAL` pro generování ID.
- `pg_catalog` pro kontrolu existujících tabulek.
- `BYTEA` pro binární data.
