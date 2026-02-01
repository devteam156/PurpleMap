# HTTP Request Handlers

## Přehled

Balíček `de.bluecolored.bluemap.common.web` obsahuje logiku pro zpracování HTTP požadavků. BlueMap nepoužívá těžký
webový server, ale sadu specializovaných handlerů, které přímo propojují URL cesty s vnitřními úložišti a suppliery.

---

# MapStorageRequestHandler.java

## Přehled

Nejdůležitější handler, který servíruje data z `MapStorage` (soubory nebo SQL).

## Vnitřní Logika: Servírování dlaždic

- **Detekce cesty:** Používá regulární výraz `tiles/([\d/]+)/x(-?[\d/]+)z(-?[\d/]+).*` k extrakci LOD úrovně a souřadnic
  X, Z.
- **Výběr úložiště:**
    - LOD 0 -> `hiresTiles()` (3D modely).
    - LOD > 0 -> `lowresTiles(lod)` (PNG obrázky).
- **Optimalizace přenosu (`writeToResponse`):**
    - Pokud jsou data v úložišti komprimovaná (např. GZIP v SQL) a prohlížeč to podporuje, pošle BlueMap komprimovaná
      data **přímo bez dekomprese**.
    - Pokud prohlížeč podporuje GZIP, ale data v úložišti komprimovaná nejsou, BlueMap je za běhu zkomprimuje.
- **Caching:** Automaticky přidává hlavičky `Cache-Control: public, max-age=86400` (1 den).

---

# FileRequestHandler.java

## Přehled

Servíruje statické soubory z webrootu (HTML, CSS, JS).

## Vnitřní Logika: Standardní web server funkce

- **Bezpečnost:** Kontroluje, zda se požadovaná cesta nachází uvnitř webrootu (`startsWith(webRoot)`). Blokuje přístup k
  souborům `.php`.
- **Výchozí soubor:** Pokud cesta ukazuje na adresář, automaticky hledá `index.html`.
- **ETag & Last-Modified:** Generuje unikátní ETag založený na velikosti souboru, hashi cesty a času poslední změny.
  Podporuje hlavičky `If-None-Match` a `If-Modified-Since` pro úsporu bandwidth (vrtací kód 304 Not Modified).

---

# RoutingRequestHandler.java

## Přehled

Implementuje stromové větvení URL cest. Umožňuje registrovat vzory (RegExp) a k nim přiřadit další handlery.

## Vnitřní Logika

- **First-Match:** Prochází registrované cesty od konce (poslední registrovaná má nejvyšší prioritu).
- **Přepisování cest:** Podporuje nahrazování částí URL (RegExp capturing groups), podobně jako mod_rewrite v Apache.

---

# MapRequestHandler.java

## Přehled

Skládá dohromady handlery pro jednu konkrétní mapu.

## Struktura Cest

- `live/players.json`: Dynamicky generovaný seznam hráčů přes `JsonDataRequestHandler` s cache limitem 1 sekunda.
- `live/markers.json`: Dynamicky generované markery s cache limitem 10 sekund.
- `.*`: Vše ostatní je předáno `MapStorageRequestHandler` (dlaždice a nastavení).
