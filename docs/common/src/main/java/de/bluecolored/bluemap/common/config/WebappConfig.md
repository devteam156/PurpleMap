# WebappConfig.java

## Přehled

`WebappConfig` definuje parametry pro webového klienta (frontend). Tato nastavení jsou BlueMapou přenášena do souboru
`settings.json` ve webrootu. Odpovídá souboru `webapp.conf`.

## Umístění

`de.bluecolored.bluemap.common.config.WebappConfig`

## Atributy

### Základní

- `enabled`: Zda se má webová aplikace generovat/aktualizovat.
- `updateSettingsFile`: Zda má BlueMap automaticky přepisovat `settings.json`.
- `webroot`: Cesta k adresáři s webovými soubory.

### Uživatelské rozhraní (Frontend Settings)

- `useCookies`: Povolení ukládání nastavení do cookies v prohlížeči.
- `defaultToFlatView`: Zda má mapa startovat v 2D režimu.
- `startLocation`: Výchozí pozice kamery (např. "world:0:64:0").
- `resolutionDefault`: Výchozí kvalita rozlišení (škálování).
- `minZoomDistance`, `maxZoomDistance`: Limity přiblížení.

### Slidery Detailů (V nastavení frontendu)

- `hiresSlider...`: Rozsahy pro detailní modely (v blocích od kamery).
- `lowresSlider...`: Rozsahy pro nízkorozlišené dlaždice.

### Cesty k datům

- `mapDataRoot`, `liveDataRoot`: Podsložky v rámci webrootu, kde klient hledá data (výchozí "maps").

### Rozšiřitelnost

- `scripts`: Množina cest k vlastním JavaScript souborům, které se mají vložit do HTML.
- `styles`: Množina cest k vlastním CSS souborům.