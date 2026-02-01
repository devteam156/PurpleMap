# TextureVariable.java

## Přehled

`TextureVariable` reprezentuje hodnotu textury v modelu. Může to být buď přímá cesta k textuře, nebo odkaz na jinou
proměnnou (např. `#all`).

## Umístění

`de.bluecolored.bluemap.core.resources.pack.resourcepack.model.TextureVariable`

## Atributy

- `referenceName`: Název odkazované proměnné (bez `#`), nebo `null` pokud jde o přímou cestu.
- `texturePath`: Cesta k textuře, nebo `null` pokud jde o nevyřešenou referenci.

## Metody

### `getTexturePath(Function<String, TextureVariable> supplier)`

Vrátí vyřešenou cestu k textuře. Pokud je proměnná referencí, rekurzivně ji vyřeší pomocí `supplier` (lookup v mapě
textur modelu).

## Vnořená třída `Adapter`

GSON adaptér, který parsuje řetězec z JSONu. Pokud začíná `#`, je to reference. Jinak je to cesta.
