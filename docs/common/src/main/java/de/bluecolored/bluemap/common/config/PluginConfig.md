# PluginConfig.java

## Přehled

`PluginConfig` obsahuje nastavení specifická pro integraci BlueMap jako pluginu/módu do Minecraft serveru. Ovládá živé
funkce jako sledování hráčů a markerů. Odpovídá souboru `plugin.conf`.

## Umístění

`de.bluecolored.bluemap.common.config.PluginConfig`

## Atributy

### Živá Mapa (Live Map)

- `livePlayerMarkers`: Zapne/vypne zobrazení hráčů na mapě.
- `hiddenGameModes`: Seznam herních módů, které se nemají zobrazovat (např. SPECTATOR).
- `hideVanished`, `hideInvisible`, `hideSneaking`: Pravidla pro schovávání hráčů.
- `hideDifferentWorld`: Schová hráče, kteří jsou v jiné dimenzi než aktuální mapa.
- `hideBelowSkyLight`, `hideBelowBlockLight`: Schová hráče v temných místech.

### Intervaly Zápisu

- `writeMarkersInterval`, `writePlayersInterval`: Čas v sekundách mezi zápisy dat na disk (pro servery bez integrovaného
  webserveru). 0 znamená zakázáno.

### Ostatní

- `skinDownload`: Povolí stahování skinů z Mojang serverů.
- `playerRenderLimit`: Omezí počet renderovaných hráčů (výkon).
- `updateCooldown`: Čas v sekundách mezi automatickými aktualizacemi mapy po změně světa (výchozí 60s).
- `fullUpdateInterval`: Čas v minutách pro vynucený kompletní update (výchozí 24h).