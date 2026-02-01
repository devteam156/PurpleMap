# ColorAdapter.java

## Přehled

`ColorAdapter` je flexibilní GSON adaptér pro `Color`. Umožňuje načítat barvy z různých formátů JSONu.

## Umístění

`de.bluecolored.bluemap.core.resources.adapter.ColorAdapter`

## Dědičnost

`TypeAdapter<Color>` -> `ColorAdapter`

## Podporované formáty pro čtení

1. **Pole čísel:** `[r, g, b, a]` nebo `[r, g, b]` (hodnoty 0.0 - 1.0).
2. **Objekt:** `{"r": 1.0, "g": 0.5, ...}`.
3. **Řetězec:** Hexadecimální kód (např. `"#FF0000"`).
4. **Číslo:** Integer reprezentující ARGB nebo RGB hodnotu.

## Formát pro zápis

Vždy zapisuje jako pole čísel `[r, g, b, a]`.
