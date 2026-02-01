# TextFormat.java

## Přehled

`TextFormat` je pomocná třída (utility class) pro formátování textových zpráv pomocí knihovny Adventure (Component API).

## Umístění

`de.bluecolored.bluemap.common.commands.TextFormat`

## Konstanty

Definuje standardní barvy (`BASE_COLOR`, `HIGHLIGHT_COLOR`, `POSITIVE_COLOR`...) a ikony používané v pluginu.

## Metody

### `format(...)`

Umožňuje formátovat zprávy pomocí placeholderu `%`. Podporuje vkládání komponent i objektů.

### `paragraph(...)`

Vytvoří formátovaný odstavec s nadpisem a obsahem.

### `details(...)`

Vytvoří stromovou strukturu detailů (pomocí ASCII znaků ├, │, └).

### `duration(...)`

Formátuje `Duration` nebo `Instant` do čitelného řetězce (např. "5 min", "2 h").

### `command(String command)`

Vytvoří klikatelnou komponentu, která spustí daný příkaz.

### `lines(...)`

Spojí více komponent oddělovačem nového řádku.
