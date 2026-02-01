# Check.java

## Přehled

`Check` je rozhraní pro implementaci různých kontrol před spuštěním akce (např. před renderováním). Používá se pro
validaci stavu, argumentů nebo konfigurace a poskytuje sjednocený způsob, jak informovat o výsledku kontroly.

## Umístění

`de.bluecolored.bluemap.common.commands.checks.Check`

## Metody

### `getResult()`

Vrátí výsledek kontroly (`CheckResult.OK` nebo `CheckResult.BAD`).

### `getFailureDescription()`

Vrátí `Component` s popisem chyby, pokud kontrola selhala.

### `test()`

Spustí kontrolu. Pokud selže (`!succeeded()`), vyhodí výjimku `CheckFailedException`.

## Vnořené třídy

- `CheckFailedException`: Výjimka, která nese informaci o tom, která kontrola selhala. Umožňuje zachytit chybu a vypsat
  uživateli relevantní zprávu.
