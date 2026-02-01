# MapStorageRequestHandler.java

## Přehled

`MapStorageRequestHandler` obsluhuje požadavky na soubory mapy (dlaždice, nastavení, assety) přímo z `MapStorage`.

## Umístění

`de.bluecolored.bluemap.common.web.MapStorageRequestHandler`

## Funkcionalita

- **Dlaždice (Tiles):** Rozpoznává vzor URL pro dlaždice (`tiles/LOD/x/z.png` nebo `.json` pro hires). Načte příslušná
  data z `GridStorage` a vrátí je.
    - Hires (LOD 0) vrací jako `application/octet-stream` (komprimované JSON/buffer data).
    - Lowres (LOD > 0) vrací jako `image/png`.
- **Metadata:** Obsluhuje požadavky na `settings.json`, `textures.json`, `live/markers.json` a `live/players.json`.
- **Assety:** Obsluhuje požadavky na `assets/...` (textury bloků atd.).
- **Komprese:** Řeší `Content-Encoding`. Pokud klient podporuje kompresi (např. gzip) a data jsou komprimovaná, pošle je
  rovnou. Pokud klient kompresi nepodporuje, data dekomprimuje.

## Metody

### `handle(HttpRequest request)`

Zpracuje požadavek na základě cesty.