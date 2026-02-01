# CommandExecutor.java

## Přehled

`CommandExecutor` je zodpovědný za vykonávání příkazů BlueMap. Zpracovává výsledek parsování (`ParseResult`), kontroluje
podmínky (např. zda je plugin načtený) a spouští příkaz.

## Umístění

`de.bluecolored.bluemap.common.commands.CommandExecutor`

## Funkcionalita

- **Asynchronní vykonávání:** Příkazy jsou spouštěny asynchronně na vláknovém poolu BlueMap (
  `CompletableFuture.supplyAsync`).
- **Předběžné kontroly:**
    - Ověřuje, zda je plugin načtený (`Commands.checkPluginLoaded`).
    - Kontroluje specifické předpoklady pro daný příkaz (`Commands.checkExecutablePreconditions`), např. oprávnění.
- **Zpracování výsledku:**
    - Čeká na výsledek příkazu (s timeoutem).
    - Pokud příkaz vrátí `ComponentLike`, odešle zprávu zdroji příkazu.
    - Vrací `1` (úspěch) nebo `0` (chyba).
- **Ošetření chyb:** Zachytává výjimky při vykonávání a loguje je.

## Vnořené třídy

- `ExecutionResult`: Záznam obsahující návratový kód (`resultCode`) a informaci, zda došlo k chybě parsování (
  `parseFailure`).
