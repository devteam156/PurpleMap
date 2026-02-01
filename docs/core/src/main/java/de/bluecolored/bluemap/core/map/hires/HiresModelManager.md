# HiresModelManager.java

## Přehled

`HiresModelManager` řídí proces renderování detailních (high-res) modelů mapy. Koordinuje jednotlivé renderovací
průchody (`RenderPass`) a ukládání výsledků.

## Umístění

`de.bluecolored.bluemap.core.map.hires.HiresModelManager`

## Atributy

- `world`: Svět, který se renderuje.
- `storage`: Úložiště pro ukládání modelů.
- `tileGrid`: Mřížka definující rozložení dlaždic.
- `renderPasses`: Kolekce renderovacích průchodů (např. pro bloky, entity). Je uložena v `ThreadLocal`, aby každý
  renderovací vlákno mělo své instance.

## Metody

### `render(Vector2i tile, TileMetaConsumer tileMetaConsumer, boolean save)`

Hlavní metoda pro vykreslení jedné dlaždice.

1. Vypočítá hranice modelu.
2. Získá instanci `ArrayTileModel` z poolu.
3. Spustí všechny `RenderPass`y, které do modelu přidají geometrii.
    - Současně `RenderPass`y volají `tileMetaConsumer` pro aktualizaci low-res mapy.
4. Pokud `save` je `true`:
    - Seřadí model (`model.sort()`).
    - Uloží model do úložiště pomocí `PRBMWriter`.
5. Vrátí model do poolu.

### `unrender(Vector2i tile, TileMetaConsumer tileMetaConsumer)`

Smaže model dlaždice z úložiště a aktualizuje `tileMetaConsumer` (vyresetuje data pro low-res mapu v dané oblasti).
