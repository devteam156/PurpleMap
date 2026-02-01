# RenderPass.java

## Přehled

`RenderPass` (renderovací průchod) je rozhraní, které zapouzdřuje logiku pro vykreslení určité části světa do modelu
dlaždice. Například může existovat průchod pro bloky, průchod pro entity, průchod pro tekutiny atd.

## Umístění

`de.bluecolored.bluemap.core.map.hires.RenderPass`

## Metody

###

`render(World world, Vector3i modelMin, Vector3i modelMax, Vector3i modelAnchor, TileModelView tileModel, TileMetaConsumer tileMetaConsumer)`

Hlavní metoda, která provádí renderování.

- **Parametry:**
    - `world`: Svět, ze kterého se čtou data.
    - `modelMin`, `modelMax`: Hranice oblasti ve světě, která se má vyrenderovat do tohoto modelu.
    - `modelAnchor`: Bod ve světě, který odpovídá bodu (0,0,0) v modelu (pro lokální souřadnice).
    - `tileModel`: Pohled na model, do kterého se má přidávat geometrie.
    - `tileMetaConsumer`: Callback pro předávání metadat (výška, barva) pro low-res mapu.

**Poznámka k vláknům:** Implementace zaručuje, že tato metoda je volána pouze jedním vláknem pro danou instanci
`RenderPass`.
