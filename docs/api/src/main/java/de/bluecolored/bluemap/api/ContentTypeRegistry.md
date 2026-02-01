# ContentTypeRegistry.java

## Přehled

`ContentTypeRegistry` je statická pomocná třída, která slouží jako registr pro mapování přípon souborů na jejich MIME
typy (Content-Type). Toto je využíváno interním webovým serverem BlueMap pro správné servírování souborů.

## Umístění

`de.bluecolored.bluemap.api.ContentTypeRegistry`

## Výchozí chování

Třída má předregistrované běžné typy souborů, jako jsou:

- Text: `txt`, `css`, `html`, `js`, `xml`, `json`, `csv`
- Obrázky: `png`, `jpg`, `gif`, `webp`, `svg`
- Audio/Video: `mp3`, `mp4`, `webm` atd.
- Fonty: `ttf`, `woff`, `woff2`

Výchozí typ pro neznámé soubory je `application/octet-stream`.

## Metody

### `fromPath(Path path)`

Odvodí Content-Type z cesty k souboru (podle jeho přípony).

### `fromFileName(String fileName)`

Odvodí Content-Type z názvu souboru.

### `fromFileSuffix(String suffix)`

Vrátí Content-Type pro danou příponu (bez tečky).

### `register(String fileSuffix, String contentType)`

Zaregistruje nový typ souboru.

- `fileSuffix`: Přípona souboru (např. "pdf").
- `contentType`: MIME typ (např. "application/pdf").

**Poznámka:** Přidané typy fungují pouze pro interní webserver BlueMap. Pokud uživatel používá externí webserver (
Apache, Nginx), musí se konfigurace provést tam.
