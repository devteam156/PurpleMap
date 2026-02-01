# LoggingRequestHandler.java

## Přehled

`LoggingRequestHandler` je wrapper (dekorátor) kolem jiného handleru, který loguje informace o každém HTTP požadavku.

## Umístění

`de.bluecolored.bluemap.common.web.LoggingRequestHandler`

## Funkcionalita

- Zdeleguje zpracování požadavku na vnitřní handler.
- Po dokončení zformátuje logovací zprávu (IP adresa, metoda, URL, status kód) a zapíše ji do loggeru.
- Respektuje `X-Forwarded-For` hlavičku pro získání IP adresy klienta za proxy.