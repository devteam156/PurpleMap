# EntityModelRenderer.java

## Přehled

`EntityModelRenderer` je hlavní třída pro vykreslování entit. Podobně jako u bloků, deleguje práci na konkrétní
renderery pro jednotlivé části entity.

## Umístění

`de.bluecolored.bluemap.core.map.hires.entity.EntityModelRenderer`

## Funkcionalita

- Používá `ResourcePack` k získání definice vzhledu entity (`EntityState`).
- Definice entity se skládá z "částí" (`Part`).
- Pro každou část najde odpovídající renderer (`EntityRenderer`) pomocí `EntityRendererType`.
- Postupně vykreslí všechny části entity do modelu.
- Aplikuje rotaci entity (yaw, pitch).

## Metody

### `render(Entity entity, BlockNeighborhood block, TileModelView tileModel)`

Vykreslí entitu.

- `entity`: Data entity (typ, pozice, rotace...).
- `block`: Blok, ve kterém entita stojí (pro světelné podmínky).
