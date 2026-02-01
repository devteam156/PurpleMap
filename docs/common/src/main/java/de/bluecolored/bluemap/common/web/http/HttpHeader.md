# HttpHeader.java

## Přehled

`HttpHeader` reprezentuje jednu HTTP hlavičku (klíč a hodnotu).

## Umístění

`de.bluecolored.bluemap.common.web.http.HttpHeader`

## Funkcionalita

- Uchovává klíč a hodnotu.
- Umí rozparsovat hodnotu na seznam hodnot (oddělených čárkou).
- Poskytuje metodu `contains(String value)` pro case-insensitive kontrolu, zda hlavička obsahuje danou hodnotu.