# SQL Command Sets & Architecture

## Přehled

BlueMap nepoužívá ORM (jako Hibernate), ale využívá přímé, vysoce optimalizované SQL dotazy. Systém je postaven na
rozhraní `CommandSet`, které definuje všechny potřebné operace, a abstraktní třídě `AbstractCommandSet`, která
implementuje logiku Java-SQL vazeb. Konkrétní dialekty pak definují pouze samotné řetězce SQL příkazů.

---

# CommandSet.java (Rozhraní)

## Přehled

Definuje kontrakt pro všechny databázové operace.

## Klíčové Skupiny Metod

- **Inicializace:** `initializeTables()` (Vytvoření tabulek).
- **Zápis/Čtení položek:** `writeItem`, `readItem` (pro metadata jako settings.json).
- **Zápis/Čtení mřížky:** `writeGridItem`, `readGridItem` (pro dlaždice mapy).
- **Správa map:** `listMapIds`, `purgeMap`, `countMapGridsItems`.
- **Iterace:** `listGridItems` (seznam souřadnic dlaždic).

---

# AbstractCommandSet.java

## Přehled

Obsahuje společnou logiku pro všechny SQL implementace. Jejím nejdůležitějším úkolem je **normalizace dat**.

## Logika Normalizace (ID Mapping)

Namísto toho, aby BlueMap v každém řádku s dlaždicí ukládala dlouhé řetězce jako "minecraft:overworld" nebo "GZIP",
používá systém číselných klíčů (IDs).

- **Cache klíčů:** Třída udržuje `LoadingCache` pro `mapKeys`, `compressionKeys`, `itemStorageKeys` a `gridStorageKeys`.
- **Princip:** Při zápisu se nejdříve zjistí číselné ID pro daný řetězec/objekt (např. mapId -> 1). Pokud v DB
  neexistuje, vytvoří se. Toto ID se pak používá jako cizí klíč v hlavních datových tabulkách.
- **Důsledek:** Drastické snížení velikosti indexů a zrychlení vyhledávání.

## Společná Logika Metod

Většina metod (např. `writeItem`) funguje následovně:

1. Získá IDs pro mapu, typ úložiště a kompresi z cache.
2. Zavolá `db.run(connection -> ...)` pro vykonání příkazu v transakci.
3. Použije `PreparedStatement` dodaný konkrétním dialektem.

---

# Databázové Schéma (Společné pro všechny dialekty)

BlueMap vytváří následující tabulky:

1. **`bluemap_map`**: Převod `map_id` (String) -> `id` (SmallInt).
2. **`bluemap_compression`**: Převod názvu komprese -> `id`.
3. **`bluemap_item_storage`**: Registry pro typy metadat.
4. **`bluemap_grid_storage`**: Registry pro typy dlaždic (hires, lowres atd.).
5. **`bluemap_item_storage_data`**: Samotná metadata (BLOB).
6. **`bluemap_grid_storage_data`**: Hlavní tabulka s dlaždicemi.
    - Sloupce: `map`, `storage`, `x`, `z`, `compression`, `data` (BLOB).
    - Primární klíč: `(map, storage, x, z)`.

---

# Dialekty (Konkrétní implementace)

### MySQLCommandSet.java

- **Specifika:** Používá `REPLACE INTO` pro efektivní "Insert or Update" operaci.
- **Kódování:** Využívá `utf8mb4_bin` pro přesné porovnávání řetězců.
- **Typy:** `LONGBLOB` pro data dlaždic.

### PostgreSQLCommandSet.java

- **Specifika:** Používá `INSERT ... ON CONFLICT (...) DO UPDATE` (standardní PostgreSQL UPSERT).
- **Typy:** `BYTEA` pro binární data, `SMALLSERIAL` pro automatické číslování ID.
- **Mazání:** Používá interní `CTID` pro limitované mazání při promazávání mapy.

### SqliteCommandSet.java

- **Specifika:** Podobné MySQL (`REPLACE INTO`).
- **Typy:** `INTEGER PRIMARY KEY AUTOINCREMENT`.
- **Režim:** Používá `STRICT` tabulky (pokud je podporováno), což zvyšuje datovou integritu.
- **Mazání:** Používá vnitřní `ROWID` pro stránkované mazání.
