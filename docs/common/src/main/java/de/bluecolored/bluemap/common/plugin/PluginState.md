# PluginState.java

## Přehled

`PluginState` je třída určená k serializaci (ukládání) stavu pluginu, který se má zachovat mezi restarty serveru. Ukládá
se do souboru `pluginState.json`.

## Umístění

`de.bluecolored.bluemap.common.plugin.PluginState`

## Ukládaná data

### `renderThreadsEnabled`

- Zda je renderování povoleno (odpovídá příkazům `/bluemap start` a `/bluemap stop`).

### `maps` (Map<String, MapState>)

- Stav jednotlivých map.
- `MapState` obsahuje:
    - `updateEnabled`: Zda je mapa aktualizována (odpovídá příkazu `/bluemap freeze`).

### `hiddenPlayers` (Set<UUID>)

- Seznam hráčů, kteří jsou skryti z mapy (pomocí API nebo příkazů).

## Metody

Gettery a settery pro výše uvedená data.
