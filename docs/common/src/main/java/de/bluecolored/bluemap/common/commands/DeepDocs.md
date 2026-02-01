# Command System

## Přehled

Balíček `de.bluecolored.bluemap.common.commands` spravuje uživatelské příkazy (např. `/bluemap update`). Celý systém je
postaven na abstrakci, která umožňuje snadnou integraci do herních enginů i konzole.

---

# Commands.java (Konfigurátor)

## Přehled

Tato třída definuje celou strukturu příkazů BlueMap. Vytváří strom podpříkazů a registruje parsery argumentů.

## Vnitřní Logika: Registrace a Kontext

- **Argument Parsers:** Učí systém, jak interpretovat složitější typy:
    - `BmMap`: Vyhledá mapu podle ID v aktuálně načtené instanci BlueMap.
    - `StorageConfig`: Vyhledá konfiguraci úložiště.
    - `RenderTask`: Používá systém **Task References** (viz níže).
- **Context Resolvers:** Automaticky dodává informace o prostředí (např. v jakém světě se nachází hráč, který příkaz
  vyvolal).
- **Anotace a Oprávnění:** Používá vlastní anotace (`@Permission`, `@WithWorld`, `@WithPosition`) k automatickému
  filtrování příkazů podle toho, co může daný uživatel dělat.

## Task References (Referenční systém)

Příkazy jako `/bluemap tasks` vypisují seznam úloh. Aby uživatel nemusel vypisovat složité ID úloh, BlueMap generuje
krátké náhodné hex kódy (např. `a1b2`).

- `RENDERTASK_TO_REF`: Cache (slabé klíče), která přiřazuje úloze kód.
- `REF_TO_RENDERTASK`: Cache (slabé hodnoty), která umožňuje vyhledat úlohu podle kódu.

---

# CommandExecutor.java

## Přehled

Zodpovídá za samotné spuštění příkazu.

## Vnitřní Logika: Asynchronní provádění

Všechny příkazy BlueMap běží asynchronně na `BlueMap.THREAD_POOL`. To je kritické, aby příkazy (které mohou trvat
dlouho, např. promazávání mapy) nezablokovaly hlavní vlákno Minecraft serveru.

- **`execute`**:
    1. Nejdříve zkontroluje, zda je BlueMap vůbec načtená (pokud příkaz není označen `@Unloaded`).
    2. Spustí příkaz v jiném vlákně.
    3. Pokud příkaz vrátí textovou zprávu (`ComponentLike`), automaticky ji pošle uživateli.
    4. Ošetřuje chyby a loguje je.

---

# BrigadierExecutionHandler.java

## Přehled

Most mezi systémem BlueMap a nativním systémem Minecraftu (**Brigadier**).

## Logika

- Převádí výsledky parsování `bluecommands` na výjimky Brigadieru (`CommandSyntaxException`).
- Díky tomu uživatel v Minecraftu vidí červené podtržení u chybných příkazů a funkční nápovědu (tab-complete).

---

# Seznam Příkazů (Přehled)

- **`update`**: Spustí aktualizaci mapy.
- **`reload`**: Znovu načte konfiguraci.
- **`status`**: Ukáže stav renderování a vytížení.
- **`tasks`**: Seznam běžících úloh.
- **`freeze` / `unfreeze`**: Pozastaví/spustí renderování konkrétní mapy.
- **`purge`**: Smaže data mapy.
