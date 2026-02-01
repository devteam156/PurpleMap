# HttpResponse.java

## Přehled

`HttpResponse` reprezentuje HTTP odpověď, která bude odeslána klientovi.

## Umístění

`de.bluecolored.bluemap.common.web.http.HttpResponse`

## Funkcionalita

- **Stav a Hlavičky:** Uchovává stavový kód (`HttpStatusCode`) a mapu hlaviček (`HttpHeader`).
- **Data:** Obsahuje data odpovědi (`data`), která mohou být nastavena jako `String`, `InputStream` nebo
  `ReadableByteChannel`.
- **Zápis:** Metoda `read(WritableByteChannel channel)` (název je z pohledu kanálu, ale zapisuje DO kanálu) postupně
  zapisuje hlavičky a data do kanálu klienta.
    - Podporuje **chunked transfer encoding**, pokud je nastaveno (automaticky přidává délky chunků).
    - Pokud není chunked, nastaví `Content-Length`.

## Metody

### `read(WritableByteChannel channel)`

Zapíše část odpovědi do výstupního kanálu. Vrací `false`, pokud zbývají další data k odeslání (buffer je plný), nebo
`true`, pokud je odpověď kompletní.

### `setData(...)`

Nastaví tělo odpovědi.