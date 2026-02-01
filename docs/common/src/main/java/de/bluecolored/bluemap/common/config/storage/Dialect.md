# Dialect.java

## Přehled

`Dialect` je rozhraní pro definici specifických dialektů SQL databází. Každý dialekt ví, jaké JDBC protokoly podporuje a
jaké SQL příkazy má generovat.

## Umístění

`de.bluecolored.bluemap.common.config.storage.Dialect`

## Implementované Dialekty

- **`MYSQL`**: Podporuje `jdbc:mysql:`, používá `MySQLCommandSet`.
- **`MARIADB`**: Podporuje `jdbc:mariadb:`, používá `MySQLCommandSet`.
- **`POSTGRESQL`**: Podporuje `jdbc:postgresql:`, používá `PostgreSQLCommandSet`.
- **`SQLITE`**: Podporuje `jdbc:sqlite:`, používá `SqliteCommandSet`.

## Metody

- `supports(String connectionUrl)`: Vrací true, pokud URL začíná protokolem dialektu.
- `createCommandSet(Database database)`: Vytvoří sadu SQL dotazů pro danou databázi.
