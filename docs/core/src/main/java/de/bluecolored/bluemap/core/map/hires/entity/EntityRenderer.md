# EntityRenderer.java

## Přehled

`EntityRenderer` je rozhraní pro komponentu, která dokáže vykreslit jednu část (Part) entity.

## Umístění

`de.bluecolored.bluemap.core.map.hires.entity.EntityRenderer`

## Metody

### `render(Entity entity, BlockNeighborhood block, Part part, TileModelView tileModel)`

Vykreslí část entity.

- `entity`: Informace o entitě.
- `block`: Blok na pozici entity.
- `part`: Definice části entity, kterou je třeba vykreslit (např. tělo, hlava, ruka).
- `tileModel`: Pohled na model, kam se má geometrie zapsat.

**Poznámka k vláknům:** Metoda je volána pouze jedním vláknem pro danou instanci rendereru.
