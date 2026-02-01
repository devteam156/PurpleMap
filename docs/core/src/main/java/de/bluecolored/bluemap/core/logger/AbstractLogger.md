# AbstractLogger.java

## Přehled

`AbstractLogger` je částečná implementace `Logger`, která se stará o logiku "anti-flood" (potlačení opakujících se
zpráv). Používá cache k pamatování si nedávno zalogovaných zpráv.

## Umístění

`de.bluecolored.bluemap.core.logger.AbstractLogger`

## Balíček

`de.bluecolored.bluemap.core.logger`

## Dědičnost

`Logger` -> `AbstractLogger`

## Atributy

### `DUMMY`

- **Typ:** `Object`
- **Popis:** Statický prázdný objekt používaný jako hodnota v mapě (cache), protože potřebujeme jen klíče.

### `noFloodCache`

- **Typ:** `com.github.benmanes.caffeine.cache.Cache<String, Object>`
- **Popis:** Cache ukládající klíče zpráv, které byly nedávno zalogovány a mají být potlačeny.
- **Konfigurace:**
    - `expireAfterWrite`: 10 minut (zpráva se může znovu objevit po 10 minutách).
    - `maximumSize`: 10 000 (aby cache nezabírala moc paměti).

## Konstruktory

### `AbstractLogger()`

Inicializuje `noFloodCache` pomocí `Caches.with()...build()`.

## Metody

### `noFloodError(String key, String message, Throwable throwable)`

- **Logika:**
    1. Zavolá privátní metodu `check(key)`.
    2. Pokud `check` vrátí `true` (klíč není v cache), zavolá abstraktní metodu `logError`.
    3. Pokud `check` vrátí `false` (klíč je v cache), zpráva je ignorována.

### `noFloodWarning(String key, String message)`

- **Logika:** Analogicky jako u `noFloodError`, volá `logWarning` pokud `check(key)` projde.

### `noFloodInfo(String key, String message)`

- **Logika:** Volá `logInfo` pokud `check(key)` projde.

### `noFloodDebug(String key, String message)`

- **Logika:** Volá `logDebug` pokud `check(key)` projde.

### `clearNoFloodLog()`

- **Popis:** Vymaže celou anti-flood cache.
- **Logika:** Volá `noFloodCache.invalidateAll()` a `cleanUp()`.

### `removeNoFloodKey(String key)`

- **Popis:** Odstraní konkrétní klíč z cache.
- **Logika:** Volá `noFloodCache.invalidate(key)`.

### `check(String key)`

- **Popis:** Privátní pomocná metoda pro kontrolu a aktualizaci cache.
- **Logika:**
    1. Zkontroluje, zda je `key` přítomen v `noFloodCache` (`getIfPresent`).
    2. Pokud **není** přítomen (`== null`):
        - Vloží ho do cache (`put(key, DUMMY)`).
        - Vrátí `true` (zpráva by se měla zalogovat).
    3. Pokud **je** přítomen:
        - Vrátí `false` (zpráva by se měla potlačit).