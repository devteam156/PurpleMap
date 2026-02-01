# Storage Systems (Core)

## Přehled

Balíček `de.bluecolored.bluemap.core.storage` definuje hierarchickou strukturu pro ukládání dat. BlueMap dělí úložiště
na tři základní úrovně:

1. **`Storage`**: Kořen systému (např. celá SQL databáze nebo složka `maps/`).
2. **`MapStorage`**: Úložiště pro jednu konkrétní mapu.
3. **`GridStorage`** / **`ItemStorage`**: Konkrétní kontejnery pro data (dlaždice, soubory).

---

# Storage.java (Rozhraní)

## Přehled

Reprezentuje hlavní instanci úložiště. Spravuje připojení a životní cyklus databáze nebo souborového systému.

## Klíčové Metody

- **`initialize()`**: Provede přípravu úložiště (např. vytvoření SQL tabulek, kontrola migrací). Volá se při startu.
- **`map(String mapId)`**: Vrátí instanci `MapStorage` pro konkrétní mapu.
- **`mapIds()`**: Vrátí stream všech ID map, které se v tomto úložišti nacházejí.

---

# MapStorage.java (Rozhraní)

## Přehled

Poskytuje přístup k různým typům dat v rámci jedné mapy. Rozlišuje mezi mřížkovými daty (dlaždice) a jednotlivými
položkami (nastavení).

## Metody (Kontejnery)

- `hiresTiles()`: `GridStorage` pro 3D modely (vysoké rozlišení).
- `lowresTiles(int lod)`: `GridStorage` pro 2D obrázky (různé úrovně detailu).
- `tileState()` / `chunkState()`: `GridStorage` pro metadata o stavu renderování a změnách v chuncích.
- `settings()`, `textures()`, `markers()`, `players()`: `ItemStorage` pro konkrétní JSON soubory mapy.

---

# GridStorage.java (Rozhraní)

## Přehled

Úložiště pro data organizovaná v nekonečné 2D mřížce (souřadnice X, Z). Každá buňka mřížky může obsahovat jeden datový
objekt (např. jednu dlaždici).

## Vnitřní Logika a Operace

- **`write(x, z)`**: Vrátí `OutputStream` pro zápis dat do buňky. Přepíše existující data.
- **`read(x, z)`**: Vrátí `CompressedInputStream` pro čtení. Pokud buňka neexistuje, vrátí `null`.
- **`stream()`**: Vrátí stream všech **existujících** buněk (`Cell`). To je klíčové pro iteraci přes mapu bez znalosti
  jejích hranic.

---

# ItemStorage.java (Rozhraní)

## Přehled

Zjednodušené úložiště pro jeden konkrétní objekt (soubor). Používá se pro metadata mapy.

## Metody

- `write()` / `read()`: Pro zápis a čtení obsahu položky.
- `exists()`: Kontrola existence.

---

# KeyedMapStorage.java (Abstraktní třída)

## Přehled

Pomocná třída, která implementuje `MapStorage` a převádí požadavky na konkrétní typy dat na volání s unikátními klíči (
`Key`).

## Vnitřní Logika

Definuje mapování:

- `hires` -> `bluemap:hires`
- `tile-state` -> `bluemap:tile-state`
- `settings.json` -> `bluemap:settings`
- ...atd.
  Implementace (SQL/File) pak musí implementovat pouze dvě metody: `grid(Key, Compression)` a `item(Key, Compression)`.
