# Commands.java

## Přehled

`Commands` je centrální třída pro definici a registraci všech příkazů BlueMap.

## Umístění

`de.bluecolored.bluemap.common.commands.Commands`

## Funkcionalita

- **Vytvoření příkazů (`create`):**
    - Inicializuje `BlueCommands` builder.
    - Registruje parsery argumentů (pro mapy, úložiště, render tasky).
    - Registruje kontextové resolvery (pro získání `ServerWorld`, `Vector3d` z `CommandSource`).
    - Registruje predikáty pro anotace `@Permission`, `@WithWorld`, `@WithPosition`.
    - Definuje strukturu příkazů a přidává podpříkazy (help, reload, purge, freeze, atd.).
- **Cache pro RenderTasky:** Udržuje slabé reference mezi `RenderTask` objekty a krátkými náhodnými ID (ref), které se
  používají v příkazech (např. pro zrušení úlohy).
- **Kontroly:**
    - `checkPluginLoaded`: Ověřuje, zda je plugin plně načten. Pokud ne, pošle zprávu uživateli.
    - `checkExecutablePreconditions`: Kontroluje podmínky před spuštěním (např. zda metoda nemá anotaci `@Unloaded`,
      která povoluje spuštění i bez načteného pluginu).

## Metody

### `create(Plugin plugin)`

Vytvoří a vrátí strom příkazů.

### `getRefForTask(...)` / `getTaskForRef(...)`

Metody pro převod mezi `RenderTask` a stringovým ID.
