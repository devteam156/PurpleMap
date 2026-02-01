# LiveMarkersDataSupplier.java

## Přehled

`LiveMarkersDataSupplier` je `Supplier<String>`, který generuje JSON data o markerech pro živou mapu (API endpoint
`/live/markers`).

## Umístění

`de.bluecolored.bluemap.common.live.LiveMarkersDataSupplier`

## Funkcionalita

- Převede mapu `MarkerSet`ů na JSON řetězec pomocí `MarkerGson`.
- Používá se pro poskytování aktuálního stavu markerů webovému klientovi.