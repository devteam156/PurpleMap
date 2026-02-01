# MySQLCommandSet.java

## Přehled

`MySQLCommandSet` je implementace `CommandSet` specifická pro MySQL a MariaDB databáze.

## Umístění

`de.bluecolored.bluemap.core.storage.sql.commandset.MySQLCommandSet`

## Dědičnost

`AbstractCommandSet` -> `MySQLCommandSet`

## SQL Dialekt

Používá specifickou syntaxi MySQL, například:

- `REPLACE INTO` pro zápis dat (upsert).
- `AUTO_INCREMENT` pro generování ID.
- `information_schema` pro kontrolu existujících tabulek.
