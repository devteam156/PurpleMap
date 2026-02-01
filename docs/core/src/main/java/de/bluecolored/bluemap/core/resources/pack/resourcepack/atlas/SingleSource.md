# SingleSource.java

## Přehled

`SingleSource` je typ zdroje v atlasu, který načte jednu konkrétní texturu.

## Umístění

`de.bluecolored.bluemap.core.resources.pack.resourcepack.atlas.SingleSource`

## Dědičnost

`Source` -> `SingleSource`

## Atributy (z JSONu)

- `resource`: Cesta k textuře.
- `sprite`: Volitelný název, pod kterým se má textura zaregistrovat (pokud se liší od `resource`).

## Metody

### `load(...)`

Načte zadanou texturu a uloží ji do poolu.
