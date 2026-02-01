# Color.java

## Přehled

Třída `Color` reprezentuje barvu v modelu RGBA (červená, zelená, modrá, průhlednost). Je používána pro definování barev
čar, výplní a dalších vizuálních prvků v BlueMap API.

## Umístění

`de.bluecolored.bluemap.api.math.Color`

## Konstruktory

### `Color(int red, int green, int blue)`

Vytvoří novou barvu s plnou neprůhledností (alpha = 1.0).

- `red`, `green`, `blue`: Hodnoty barevných složek v rozsahu 0-255.

### `Color(int red, int green, int blue, float alpha)`

Vytvoří novou barvu s definovanou průhledností.

- `alpha`: Průhlednost v rozsahu 0.0 (plně průhledné) až 1.0 (plně neprůhledné).

### `Color(int i)`

Vytvoří barvu z celého čísla ve formátu `0xAARRGGBB` (Alpha, Red, Green, Blue).

### `Color(int i, float alpha)`

Vytvoří barvu z celého čísla ve formátu `0xRRGGBB` a explicitní hodnoty alpha (0.0 - 1.0).

### `Color(int i, int alpha)`

Vytvoří barvu z celého čísla ve formátu `0xRRGGBB` a explicitní hodnoty alpha (0 - 255).

### `Color(String cssColorString)`

Vytvoří barvu z CSS řetězce.

- Podporované formáty: `#RRGGBB`, `#RRGGBBAA`, `#RGB`, `#RGBA`.
- Může vyhodit `NumberFormatException`, pokud je formát neplatný.

## Metody

### `getRed()`

Vrací červenou složku barvy (0-255).

### `getGreen()`

Vrací zelenou složku barvy (0-255).

### `getBlue()`

Vrací modrou složku barvy (0-255).

### `getAlpha()`

Vrací alpha složku (průhlednost) barvy (0.0 - 1.0).

### `equals(Object o)`

Porovnává barvu s jiným objektem.

### `hashCode()`

Vrací hash kód barvy.

### `toString()`

Vrací textovou reprezentaci instance třídy `Color`.
