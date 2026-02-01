# ServerWorld.java

## Přehled

`ServerWorld` je rozhraní reprezentující svět na serveru z pohledu serverové implementace.

## Umístění

`de.bluecolored.bluemap.common.serverinterface.ServerWorld`

## Metody

### `getWorldFolder()`

Vrací cestu k adresáři světa (tam, kde jsou `region` soubory).

### `getDimension()`

Vrací identifikátor dimenze (`Key`), např. `minecraft:overworld`.

### `persistWorldChanges()`

Pokusí se vynutit uložení změn ve světě na disk (save).

- Vrací `true`, pokud se uložení zdařilo.
- Vrací `false`, pokud operace není podporována.
- Vyhodí `IOException` při chybě.
