# Custom IO Streams

## Přehled

Sada tříd v balíčku `de.bluecolored.bluemap.core.util.stream`, které obalují standardní `InputStream` a `OutputStream` a
přidávají jim specifickou logiku (dekorátory).

## Třídy

### `DelegateInputStream` & `DelegateOutputStream`

- **Účel:** Základní třídy pro vytváření dekorátorů streamů.
- **Logika:** Všechny metody (read, write, close, skip...) jednoduše přeposílají volání vnitřnímu streamu (`in` /
  `out`). Ostatní třídy z nich dědí a přepisují jen to, co potřebují změnit.

### `CountingOutputStream`

- **Účel:** Sledování množství zapsaných dat.
- **Logika:** Při každém volání `write()` inkrementuje vnitřní čítač `count` o počet zapsaných bajtů. BlueMap to používá
  pro statistiky a logování velikosti generovaných souborů.

### `OnCloseOutputStream`

- **Účel:** Vykonání akce po uzavření streamu.
- **Logika:** Přepisuje metodu `close()`. Nejdříve zavře vnitřní stream a poté zavře (spustí) objekt
  `AutoCloseable onClose`.
- **Použití:** Klíčové pro `FileHelper.createFilepartOutputStream`. Akce `onClose` zde provádí atomický přesun souboru z
  dočasného umístění do finálního cíle.

---

# NBT Adapters

## Přehled

Třídy v balíčku `de.bluecolored.bluemap.core.util.nbt`, které integrují knihovnu BlueNBT se systémy BlueMap (Registry,
Key).

## Třídy

### `RegistryAdapter<T>`

- **Účel:** Umožňuje přímo ukládat a načítat objekty z registrů BlueMap do NBT (např. typy úloh, biomy).
- **Logika:**
    - **Zápis:** Zapíše formátovaný klíč objektu (`key.getFormatted()`) jako NBT String.
    - **Čtení:** Přečte string, převede ho na `Key` a vyhledá objekt v příslušném `Registry`. Pokud objekt neexistuje,
      vrátí `fallback` hodnotu.

### `PalettedArrayAdapter<T>`

- **Účel:** Implementace paletizovaného pole v NBT.
- **Formát v NBT:** Objekt se dvěma poli: `palette` (seznam unikátních prvků) a `data` (pole bajtů s indexy do palety).
- **Logika:**
    - **Čtení:** Nejdříve načte paletu a data. Poté vytvoří pole typu `T` a pro každý index v datech tam vloží
      odpovídající prvek z palety.
    - **Zápis:** Automaticky vygeneruje paletu unikátních prvků z předaného pole a vytvoří pole indexů (data). Výrazně
      šetří místo, pokud se prvky v poli opakují.
