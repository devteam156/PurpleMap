# FileRequestHandler.java

## Přehled

`FileRequestHandler` slouží k poskytování statických souborů z disku (typicky webroot s frontend aplikací).

## Umístění

`de.bluecolored.bluemap.common.web.FileRequestHandler`

## Funkcionalita

- **Bezpečnost:** Kontroluje, zda požadovaný soubor leží uvnitř `webRoot` adresáře (brání Path Traversal útokům).
  Zakazuje přístup k `.php` souborům.
- **Index:** Pokud je požadován adresář, zkouší vrátit `index.html`.
- **Caching:** Podporuje `If-Modified-Since` a `If-None-Match` (ETag) hlavičky pro efektivní cachování v prohlížeči (
  vrací `304 Not Modified`).
- **MIME Types:** Určuje `Content-Type` podle přípony souboru.

## Metody

### `handle(HttpRequest request)`

Obslouží GET požadavek na soubor.