# BlueMapResponseModifier.java

## Přehled

`BlueMapResponseModifier` je dekorátor, který upravuje HTTP odpovědi (přidává hlavičky, formátuje chybové stránky).

## Umístění

`de.bluecolored.bluemap.common.web.BlueMapResponseModifier`

## Funkcionalita

- Přidá hlavičku `Server: BlueMap/VERZE`.
- Pokud je status kód chybový (>= 400) a odpověď nemá tělo, vloží do těla jednoduchou chybovou zprávu.