# RenderManagerImpl.java

## Přehled

`RenderManagerImpl` implementuje veřejné rozhraní `RenderManager`. Zprostředkovává ovládání interního
`de.bluecolored.bluemap.common.rendermanager.RenderManager`.

## Umístění

`de.bluecolored.bluemap.common.api.RenderManagerImpl`

## Implementovaná Rozhraní

`RenderManager`

## Metody

### `scheduleMapUpdateTask(BlueMapMap map, boolean force)`

Naplánuje aktualizaci mapy. Vytvoří `MapUpdatePreparationTask` s strategií `TileUpdateStrategy.fixed(force)`.

### `scheduleMapUpdateTask(BlueMapMap map, Collection<Vector2i> regions, boolean force)`

Naplánuje aktualizaci konkrétních regionů. Vytvoří přímo `MapUpdateTask`.

### `scheduleMapPurgeTask(BlueMapMap map)`

Naplánuje vymazání mapy (`MapPurgeTask`).

### `renderQueueSize()`

Deleguje na interní `getScheduledRenderTaskCount()`.

### `renderThreadCount()`

Deleguje na interní `getWorkerThreadCount()`.

### `isRunning()`

Vrací stav interního render manageru.

### `start()`

Spustí renderer s počtem vláken definovaným v konfiguraci (`core.conf`). Nastaví stav pluginu `RenderThreadsEnabled` na
`true`.

### `start(int threadCount)`

Spustí renderer s explicitním počtem vláken.

### `stop()`

Zastaví renderer a nastaví stav pluginu `RenderThreadsEnabled` na `false`.
