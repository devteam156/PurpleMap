# TileUpdateStrategy.java

## Přehled

`TileUpdateStrategy` je funkcionální rozhraní používané k rozhodování, zda se má dlaždice (tile) přerenderovat, i když
se její zdrojová data (chunky) nezměnila.

## Umístění

`de.bluecolored.bluemap.common.rendermanager.TileUpdateStrategy`

## Rozhraní

Dědí od `java.util.function.Predicate<TileState>`.

## Předdefinované Implementace (Konstanty)

### `FORCE_ALL`

Vždy vrací `true`. Vynutí update všech dlaždic bez ohledu na stav. Používá se při volání s příznakem `--force`.

### `FORCE_EDGE`

Vrací `true` pouze pokud je stav dlaždice `RENDERED_EDGE`. To se používá pro opravu okrajů mapy, kde mohou chybět data z
okolních regionů.

### `FORCE_NONE`

Vždy vrací `false`. Update se provede pouze tehdy, pokud BlueMap detekuje změnu v chuncích (pomocí hashů).

## Statické Metody

### `fixed(boolean force)`

Pomocná metoda, která vrátí `FORCE_ALL` pokud je parametr true, jinak `FORCE_NONE`.
