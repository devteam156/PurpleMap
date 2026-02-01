# ConfigurationException.java

## Přehled

`ConfigurationException` je výjimka používaná v celém projektu pro signalizaci chyb v konfiguraci. Poskytuje přívětivé
vysvětlení chyby pro uživatele.

## Umístění

`de.bluecolored.bluemap.common.config.ConfigurationException`

## Dědičnost

`Exception` -> `ConfigurationException`

## Vlastnosti

- **explanation**: Srozumitelný text vysvětlující, co je špatně a jak to opravit.

## Metody

### `getRootCause()`

Najde původní příčinu (root cause) výjimky, přičemž přeskakuje vnořené `ConfigurationException`.

### `getFullExplanation()`

Rekurzivně sestaví vysvětlení ze všech zřetězených (chained) `ConfigurationException`.

### `getFormattedExplanation()`

Vrátí vysvětlení zformátované do bloku s oddělovači (`####`), připravené pro výpis do logu/konzole.

### `printLog(Logger logger)`

Vypíše zformátované vysvětlení do loggeru jako varování (`logWarning`). Pokud existuje i technická příčina (jiná
výjimka), vypíše ji jako chybu (`logError`).
