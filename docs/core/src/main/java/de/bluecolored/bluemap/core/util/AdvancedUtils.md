# WatchService.java (Rozhraní)

## Přehled

Generické rozhraní pro služby, které sledují změny a poskytují proud událostí. BlueMap ho používá například pro
sledování změn v souborech regionů.

## Umístění

`de.bluecolored.bluemap.core.util.WatchService`

## Metody

### `poll()`

- **Popis:** Okamžitě se pokusí získat další dávku událostí.
- **Logika:** Nečeká. Pokud nejsou žádné události, vrátí `null`.

### `poll(long timeout, TimeUnit unit)`

- **Popis:** Čeká na události po zadanou dobu.
- **Logika:** Pokud do vypršení limitu nic nepřijde, vrátí `null`.

### `take()`

- **Popis:** Blokující metoda.
- **Logika:** Čeká nekonečně dlouho, dokud není k dispozici alespoň jedna událost.

## Vnořené třídy

- `ClosedException`: Výjimka vyhozená při pokusu o operaci na již uzavřené službě.

---

# Tristate.java (Enum)

## Přehled

Reprezentuje logickou hodnotu se třemi stavy: `TRUE`, `FALSE` a `UNDEFINED`. Používá se tam, kde potřebujeme odlišit "
vypnuto" od "nenastaveno" (např. u vlastností bloků).

## Umístění

`de.bluecolored.bluemap.core.util.Tristate`

## Hodnoty a Logika

- **`TRUE`**: Reprezentuje logickou pravdu.
- **`FALSE`**: Reprezentuje logickou nepravdu.
- **`UNDEFINED`**: Reprezentuje neurčený stav.

### Logické operátory

Enum implementuje vlastní metody pro logické operace, které berou v úvahu `UNDEFINED`:

- **`and`**:
    - `TRUE and X -> X`
    - `FALSE and X -> FALSE`
    - `UNDEFINED and FALSE -> FALSE`, jinak `UNDEFINED`
- **`or`**:
    - `TRUE or X -> TRUE`
    - `FALSE or X -> X`
    - `UNDEFINED or TRUE -> TRUE`, jinak `UNDEFINED`

## Metody

- `getOr(defaultValue)`: Vrátí hodnotu nebo výchozí hodnotu, pokud je stav `UNDEFINED`.
- `negated()`: Vrátí opačný stav (UNDEFINED zůstává UNDEFINED).
- `valueOf(boolean)`: Statická metoda pro převod z klasického booleanu.

---

# Vector2iCache.java

## Přehled

Extrémně rychlá, nízkoúrovňová cache pro instance `Vector2i`. Slouží k recyklaci objektů souřadnic, aby se snížila zátěž
Garbage Collectoru (GC pressure).

## Umístění

`de.bluecolored.bluemap.core.util.Vector2iCache`

## Logika a Algoritmus

- **Struktura:** Používá fixní pole o velikosti 16 384 (`0x4000`) prvků.
- **Hashování:** Index do pole se vypočítá jako `(x * 1456 ^ y * 948375892) & 0x3FFF`. Jde o velmi rychlou XOR operaci s
  magickými čísly.
- **Získání (`get`):**
    1. Vypočítá index.
    2. Zkontroluje, zda na indexu leží vektor se stejnými X a Z.
    3. Pokud ano, vrátí existující instanci.
    4. Pokud ne, vytvoří novou instanci, uloží ji na index (přepíše starou) a vrátí ji.
- **Výsledek:** Tato cache nezaručuje, že pro stejná X, Z vždy vrátí stejnou instanci (může dojít ke kolizi a přepsání),
  ale drasticky snižuje počet alokací nových objektů v kritických smyčkách.

---

# StringUtil.java

## Přehled

Pomocná třída pro optimalizaci práce s řetězci.

## Umístění

`de.bluecolored.bluemap.core.util.StringUtil`

## Funkcionalita

- **`intern(String)`**: Používá `Interner` z knihovny Caffeine s "Weak" referencemi.
- **Proč?**: Standardní `String.intern()` v Javě je pomalý a plní PermGen/Metaspace, který se špatně čistí. Caffeine
  Interner je mnohem rychlejší a bezpečnější pro paměť. BlueMap ho používá pro identifikátory (klíče), aby ušetřila RAM.

---

# Lazy.java (Generická třída)

## Přehled

Implementace líné (lazy) inicializace objektu. Objekt je vytvořen až v momentě prvního přístupu.

## Umístění

`de.bluecolored.bluemap.core.util.Lazy`

## Funkcionalita

- **Thread-Safety:** Používá vzor **Double-Checked Locking** s `volatile` proměnnou, což zaručuje, že inicializační
  funkce (`loader`) bude zavolána právě jednou i při přístupu z více vláken.
- **Uvolnění loaderu:** Po úspěšném načtení nastaví odkaz na `loader` na `null`, aby mohl být uvolněn z paměti.

---

# MergeSort.java

## Přehled

Vlastní implementace algoritmu MergeSort optimalizovaná pro pole primitivních integerů. Adaptováno z knihovny
`fastutil`.

## Umístění

`de.bluecolored.bluemap.core.util.MergeSort`

## Logika

- **Hybridní přístup:** Pokud je pole menší než 16 prvků, použije **Insertion Sort**, který je pro malé sady dat
  rychlejší.
- **Rekurze:** Pro větší pole se rekurzivně dělí na poloviny, třídí a následně slévá (merge).
- **Stabilita:** MergeSort je stabilní algoritmus (zachovává pořadí prvků se stejným klíčem).
