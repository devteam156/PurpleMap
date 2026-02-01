# SQL Storage System

## Přehled

Balíček `de.bluecolored.bluemap.core.storage.sql` implementuje rozhraní `Storage` nad relačními databázemi. Celý systém
je navržen tak, aby byl nezávislý na konkrétním typu DB (MySQL, PostgreSQL, SQLite) díky abstrakci `CommandSet`.

---

# SQLStorage.java

## Přehled

Vstupní bod do SQL úložiště. Spravuje cache pro `SQLMapStorage` a zajišťuje inicializaci tabulek.

## Atributy

- `sql`: `CommandSet` - Sada SQL příkazů pro daný dialekt.
- `mapStorages`: `LoadingCache<String, SQLMapStorage>` - Cache pro instance úložišť jednotlivých map.

## Vnitřní Logika a Metody

### `mapIds()`

- **Logika:** Vrací stream ID map. Protože map může být hodně, používá `PageSpliterator`, který načítá ID po stránkách (
  1000 kusů najednou) voláním `sql.listMapIds`. Tím brání zahlcení paměti.

---

# SQLMapStorage.java

## Přehled

Zpracovává požadavky na data v rámci jedné mapy v databázi.

## Vnitřní Logika a Metody

### `delete(DoublePredicate onProgress)`

- **Logika:** Implementuje bezpečné a sledovatelné mazání mapy z DB.
    1. Zjistí celkový počet dlaždic (`sql.countMapGridsItems`).
    2. V cyklu maže dlaždice po dávkách (1000 kusů) voláním `sql.purgeMapGrids`.
    3. Po každé dávce aktualizuje `onProgress`.
    4. Nakonec smaže i záznam o mapě v tabulce map (`sql.purgeMap`).

---

# SQLGridStorage.java

## Přehled

Ukládá mřížková data (tiles) do SQL tabulky. Každá dlaždice je uložena jako BLOB (Binary Large Object).

## Vnitřní Logika a Metody

### `write(x, z)`

- **Logika:** Používá `OnCloseOutputStream`.
    1. Data se nejdříve komprimují do `ByteArrayOutputStream` v paměti.
    2. Při zavření streamu (`onClose`) se celý bajtový balík zapíše do DB jediným SQL dotazem `writeGridItem`. Tím se
       minimalizuje počet otevřených transakcí.

### `stream()`

- **Logika:** Umožňuje iterovat přes všechny dlaždice v DB. Opět používá `PageSpliterator` pro stránkování výsledků, což
  je nezbytné, protože mapa může mít miliony dlaždic.

---

# Database.java

## Přehled

Spravuje nízkoúrovňové připojení k databázi (JDBC). Implementuje **Connection Pooling** pomocí knihovny Apache Commons
DBCP2.

## Vnitřní Logika a Konfigurace

- **Pooling:** Udržuje pool otevřených spojení (`PoolingDataSource`).
- **Pravidla pro spojení:**
    - `autoCommit = false`: BlueMap striktně řídí transakce.
    - `fastFailValidation = true`: Rychle detekuje rozbitá spojení.
    - `maxIdle`: Odpovídá počtu jader CPU (optimální pro paralelní renderování).

### `run(ConnectionFunction<R> action)`

- **Klíčová logika:** Vykoná databázovou operaci s automatickým Retry mechanismem.
- Pokud operace vyhodí `SQLRecoverableException` (dočasná chyba spojení), zkusí akci ještě jednou s novým spojením z
  poolu.
- Po úspěšném dokončení automaticky provede `connection.commit()`.

---

# PageSpliterator.java

## Přehled

Vlastní implementace `Spliterator`u pro stránkované čtení z databáze.

## Logika

Udržuje aktuální stránku a pozici v ní. Jakmile dojde na konec pole `lastBatch`, zavolá `pageSupplier` pro načtení další
stránky. Tím převádí asynchronní/stránkovaný API databáze na standardní Java `Stream`.
