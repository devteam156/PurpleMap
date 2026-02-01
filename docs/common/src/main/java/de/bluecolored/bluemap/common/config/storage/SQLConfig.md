# SQLConfig.java

## Přehled

`SQLConfig` obsahuje detailní nastavení pro ukládání mapy do SQL databáze. Zpracovává připojení, dialekty a dynamické
načítání ovladačů (JDBC driverů).

## Umístění

`de.bluecolored.bluemap.common.config.storage.SQLConfig`

## Atributy

### Připojení

- `connectionUrl`: JDBC URL (např. `jdbc:mysql://localhost/bluemap`).
- `connectionProperties`: Mapa dodatečných vlastností pro JDBC spojení (např. jméno, heslo).
- `maxConnections`: Maximální počet současných spojení v poolu.

### Dialekt a Ovladač

- `dialect`: Typ SQL databáze (mysql, postgresql, sqlite). Pokud je `null`, BlueMap se pokusí dialekt detekovat z
  `connectionUrl`.
- `driverJar`: Cesta k externímu JAR souboru s JDBC ovladačem.
- `driverClass`: Plné jméno třídy ovladače (např. `com.mysql.cj.jdbc.Driver`).

### Data

- `compression`: Typ komprese pro data v DB (výchozí GZIP).

## Vnitřní Logika a Metody

### `createStorage()`

1. **Vytvoření ovladače:** Zavolá `createDriver()`.
2. **Inicializace databáze:** Vytvoří objekt `Database` s URL a parametry.
3. **Vytvoření příkazů:** Podle dialektu vytvoří `CommandSet` (sadu SQL dotazů optimalizovanou pro danou DB).
4. Vrátí novou instanci `SQLStorage`.

### `createDriver()` (Privátní)

- **Logika:** Pokud je zadán `driverJar`, vytvoří nový `URLClassLoader`, načte třídu z JARu a vytvoří její instanci. Tím
  BlueMap umožňuje používat libovolné databáze bez nutnosti mít jejich ovladače v základní instalaci.

### `getDialect()`

- **Logika:** Pokud není dialekt v configu, prohledá `Dialect.REGISTRY` a zkusí najít ten, který podporuje zadanou
  `connectionUrl`.