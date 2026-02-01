# ConfigTemplate.java

## Přehled

`ConfigTemplate` je jednoduchý, ale výkonný systém pro generování textových konfiguračních souborů. Podporuje
nahrazování proměnných a podmíněné bloky textu.

## Umístění

`de.bluecolored.bluemap.common.config.ConfigTemplate`

## Syntaxe Šablon

### Proměnné

Zapisují se jako `${jmeno-promenne}`. Jsou nahrazeny hodnotou nastavenou přes `setVariable`.

### Podmínky

Zapisují se jako `${podminka<< ... text ... >>}`. Text uvnitř závorek se do výsledku zahrne pouze v případě, že podmínka
byla aktivována přes `setConditional(podminka, true)`. Podmínky mohou být vnořené.

## Metody

### `setVariable(String variable, String value)`

Nastaví hodnotu proměnné. Hodnota je automaticky ošetřena (`replacerEscape`), aby se zabránilo problémům s dolary a
zpětnými lomítky.

### `setConditional(String conditional, boolean enabled)`

Zapne nebo vypne podmíněný blok.

### `build()`

Provede proces nahrazení.

1. Nejdříve rekurzivně vyřeší podmíněné bloky (pomocí regulárního výrazu `TEMPLATE_CONDITIONAL`).
2. Poté do výsledku dosadí všechny proměnné (přes `TEMPLATE_VARIABLE`).
3. Pokud proměnná není definována, nahradí ji otazníkem `?`.

### `replacerEscape(String raw)`

Privátní pomocná metoda, která escapuje znaky `\` a `$`, aby nebyly chybně interpretovány regulárním výrazem při
nahrazování.

- `\` -> `\\`
- `$` -> `\$`