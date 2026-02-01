# MaskType.java

## Přehled

`MaskType` je registr podporovaných geometrických tvarů masek. Definuje mapování mezi klíčem v konfiguraci a příslušnou
konfigurační třídou.

## Umístění

`de.bluecolored.bluemap.common.config.mask.MaskType`

## Registrované Typy

- **`BOX`**: Kvádr (definovaný min/max souřadnicemi X, Y, Z).
- **`CIRCLE`**: Kruh (střed X, Z a poloměr).
- **`ELLIPSE`**: Elipsa (střed X, Z a dva poloměry).
- **`POLYGON`**: Obecný polygon (seznam bodů X, Z).
- **`BLUR`**: Rozostření okrajů jiné masky.

## Metody

- `getConfigType()`: Vrátí třídu konfigurace (např. `PolygonMaskConfig.class`) pro daný typ masky.