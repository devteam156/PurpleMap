# MaskConfig.java

## Přehled

`MaskConfig` je abstraktní základ pro všechny konfigurace masek. Obsahuje společnou logiku pro typování masek a umožňuje
jejich sčítání nebo odčítání v rámci složených masek.

## Umístění

`de.bluecolored.bluemap.common.config.mask.MaskConfig`

## Balíček

`de.bluecolored.bluemap.common.config.mask`

## Atributy

- `type`: `String` - Identifikátor typu masky (výchozí "box").
- `subtract`: `boolean` (Výchozí: `false`) - Pokud je true, tato maska bude z celkové vyrenderované oblasti **odečtena
  ** (vytvoří "díru"). Pokud false, bude k oblasti **přidána**.

## Metody

### `getMaskType()`

- **Logika:** Převede textový řetězec `type` na objekt `MaskType` pomocí registru.

### `createMask()`

- **Popis:** Abstraktní tovární metoda. Musí vrátit instanci geometrické masky z jádra (
  `de.bluecolored.bluemap.core.map.mask.Mask`).

### `addTo(CombinedMask combinedMask)`

- **Logika:**
    1. Vytvoří instanci masky voláním `createMask()`.
    2. Přidá ji do složené masky `combinedMask`.
    3. Respektuje příznak `subtract`.