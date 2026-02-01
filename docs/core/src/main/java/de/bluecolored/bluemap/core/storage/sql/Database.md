# Database.java

## Přehled

`Database` je wrapper kolem `javax.sql.DataSource`, který spravuje připojení k databázi. Používá knihovnu Apache Commons
DBCP2 pro connection pooling.

## Umístění

`de.bluecolored.bluemap.core.storage.sql.Database`

## Implementovaná Rozhraní

`Closeable`

## Konstruktory

- S URL a vlastnostmi (najde ovladač automaticky pomocí `DriverManager`).
- S URL, vlastnostmi a instancí `Driver` (pro případy, kdy je ovladač načten dynamicky z JARu).

## Funkcionalita

- **Connection Pooling:** Vytváří pool připojení s nastavitelnou velikostí, testováním připojení a automatickým
  reconnectem.
- **Transakce:** V metodě `run` automaticky spravuje transakce (commit/rollback).
- **Retry:** Pokud operace selže s `SQLRecoverableException`, pokusí se ji zopakovat (max 2x).

## Metody

### `run(ConnectionFunction<R> action)`

Spustí akci s platným připojením k databázi.

- Získá připojení z poolu.
- Spustí `action.apply(connection)`.
- Pokud akce proběhne v pořádku, provede `commit`.
- Pokud dojde k chybě, provede `rollback` (automaticky pool nastavením `setRollbackOnReturn`).
- Pokud dojde k výpadku spojení, pokusí se akci zopakovat.
