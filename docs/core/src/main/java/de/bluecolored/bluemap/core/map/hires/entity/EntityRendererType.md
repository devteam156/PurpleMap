# EntityRendererType.java

## Přehled

`EntityRendererType` je registr a identifikátor typů rendererů entit.

## Umístění

`de.bluecolored.bluemap.core.map.hires.entity.EntityRendererType`

## Implementovaná Rozhraní

`Keyed`, `EntityRendererFactory`

## Konstanty / Registry

- `DEFAULT`: Standardní renderer pro entity definované v resource packu (`ResourceModelRenderer`).
- `MISSING`: Renderer pro chybějící entity (`MissingModelRenderer`).
- `REGISTRY`: Registr všech dostupných typů.

## Metody

### `isFallbackFor(Key entityType)`

Určuje, zda tento typ rendereru může sloužit jako záloha pro daný typ entity, pokud pro něj neexistuje resource.

### `create(...)`

Deleguje na vnitřní továrnu.
