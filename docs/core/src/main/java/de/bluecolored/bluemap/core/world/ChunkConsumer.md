# ChunkConsumer.java

## Přehled

`ChunkConsumer` je rozhraní pro konzumaci (zpracování) načtených chunků z regionu. Umožňuje filtrovat chunky, které se
mají načíst, a následně je zpracovat.

## Umístění

`de.bluecolored.bluemap.core.world.ChunkConsumer`

## Generika

- `<T>`: Typ chunku (např. `Chunk` nebo `MCAChunk`).

## Metody

### `filter(int chunkX, int chunkZ, int lastModified)`

Rozhoduje, zda se má chunk načíst.

- Pokud vrátí `true`, chunk se načte a předá metodě `accept`.
- Pokud vrátí `false`, chunk se přeskočí (úspora I/O a paměti).
- `lastModified`: Timestamp poslední úpravy chunku.

### `accept(int chunkX, int chunkZ, T chunk)`

Zpracuje načtený chunk.

### `fail(int chunkX, int chunkZ, IOException exception)`

Volá se, pokud dojde k chybě při načítání chunku. Výchozí implementace vyhodí výjimku dál.

## Vnořené rozhraní `ListOnly`

Specializovaný consumer, který načítá pouze metadata o existenci a čase změny chunku, ale ne samotná data chunku (metoda
`accept` vyhazuje výjimku).
