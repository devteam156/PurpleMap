# MapConfig.java

## Přehled

`MapConfig` definuje parametry pro konkrétní vyrenderovanou mapu. Tato třída implementuje rozhraní `MapSettings`, které
používá jádro pro řízení procesu renderování. Odpovídá souborům ve složce `maps/`.

## Umístění

`de.bluecolored.bluemap.common.config.MapConfig`

## Klíčové Atributy

### Zdroj dat a identifikace

- `world`: Cesta ke složce se světem (regiony).
- `dimension`: Identifikátor dimenze (např. `minecraft:overworld`).
- `name`: Lidsky čitelný název mapy.
- `sorting`: Číslo pro řazení v menu (nižší dříve).

### Vizuální nastavení

- `startPos`: Počáteční souřadnice kamery.
- `skyColor`, `voidColor`: Barvy oblohy a prázdna (v hex formátu).
- `ambientLight`: Intenzita okolního světla (0.0 až 1.0).
- `skyLight`: Intenzita slunečního světla.

### Logika renderování (Caves & Light)

- `removeCavesBelowY`: Bloky pod touto výškou jsou považovány za jeskyně (pokud jsou zakryté).
- `caveDetectionOceanFloor`: Výška "dna oceánu" pro algoritmus detekce jeskyní.
- `caveDetectionUsesBlockLight`: Zda se má pro detekci jeskyní používat úroveň světla z bloků (nejen oblohy).
- `ignoreMissingLightData`: Povolí renderování i bez vypočteného světla v chuncích.

### Filtrování a Výkon

- `renderMask`: Definice oblastí, které se mají (ne)renderovat.
- `minInhabitedTime`: Minimální čas (v ticích), který museli hráči v chunku strávit, aby byl vyrenderován.
- `minInhabitedTimeRadius`: Rozšíření kontroly inhabited-time na sousední chunky.
- `renderEdges`: Zda renderovat i okraje nezměněných oblastí.
- `checkForRemovedRegions`: Zda při startu hledat a mazat regiony, které byly odstraněny ze světa.

### Ovládání WebApp

- `enablePerspectiveView`, `enableFlatView`, `enableFreeFlightView`: Přepínače režimů kamery.
- `enableHires`: Povolení detailních 3D modelů.

### Interní (Skryté)

- `hiresTileSize`, `lowresTileSize`, `lodCount`, `lodFactor`: Technické parametry mřížky mapy (velikost dlaždic a úrovně
  detailů).

## Metody

### `parseMarkerSets()`

- **Logika:** Převede složitou strukturu markerů z formátu HOCON na JSON a poté pomocí `MarkerGson` (z API) vytvoří
  objekty `MarkerSet`. Tím je zajištěna kompatibilita mezi konfigurací a API.

### `checkLegacy()`

- **Logika:** Kontroluje, zda v konfiguraci nejsou staré parametry (`minX`, `maxX` atd.). Pokud ano, vyhodí výjimku s
  odkazem na návod k upgradu.