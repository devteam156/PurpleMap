# Text.java

## Přehled

Třída `Text` slouží k vytváření a formátování textových zpráv v Minecraft stylu (podobně jako `TextComponent` v Bukkitu
nebo Adventure API). Podporuje barvy, formátování, hover eventy a click eventy.

## Umístění

`de.bluecolored.bluemap.common.plugin.text.Text`

## Funkcionalita

- Umožňuje skládat text z komponent (children).
- Podporuje serializaci do JSON formátu (pro použití v příkazech, jako je `/tellraw`).
- Podporuje konverzi do formátovaného řetězce s legacy kódy (např. `§cText`).

## Metody

### `of(String message)` / `of(TextColor color, String message)` / `of(Object... objects)`

Statické tovární metody pro snadné vytvoření textu. `of(Object...)` je velmi flexibilní a umožňuje kombinovat řetězce,
barvy a formáty v jednom volání.

### `setHoverText(Text hoverText)`

Nastaví text, který se zobrazí při najetí myší.

### `setClickAction(ClickAction action, String value)`

Nastaví akci po kliknutí (např. otevření URL, spuštění příkazu).

### `addChild(Text child)`

Přidá podřízený text.

### `toJSONString()`

Vrátí JSON reprezentaci textu (kompatibilní s Minecraft chat JSON formátem).

### `toFormattingCodedString(char escapeChar)`

Vrátí legacy řetězec s formátovacími kódy (např. pomocí znaku `§`).

### `toPlainString()`

Vrátí čistý text bez formátování.
