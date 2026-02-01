# HTTP Server Architecture (NIO Stack)

## Přehled

Balíček `de.bluecolored.bluemap.common.web.http` obsahuje kompletní, asynchronní implementaci HTTP serveru. Server je
postaven na neblokujícím I/O (NIO), což znamená, že nepoužívá jedno vlákno na jedno spojení, ale využívá `Selector` k
efektivní správě mnoha otevřených soketů najednou.

---

# Server.java (Základní asynchronní server)

## Přehled

Abstraktní základ pro jakýkoli síťový server v BlueMap. Běží ve vlastním vlákně.

## Vnitřní Logika: NIO Loop

- **Selector:** Centrální bod, který sleduje události na všech registrovaných kanálech (příchozí spojení, připravenost
  ke čtení/zápisu).
- **`run()`**: Nekonečná smyčka, která volá `selector.select(...)`.
- **`accept(...)`**: Pokud se připojí nový klient, server vytvoří `SocketChannel`, přepne ho do neblokujícího režimu a
  zaregistruje ho u selektoru pro operace čtení i zápisu. Ke každému spojení je připojen "attachment" typu
  `SelectionConsumer` (zde `HttpConnection`).

---

# HttpServer.java

## Přehled

Konkrétní implementace serveru pro protokol HTTP.

## Vnitřní Logika

Jednoduše rozšiřuje `Server` a jako connection handler vytváří instance `HttpConnection`, kterým předává centrální
`HttpRequestHandler`.

---

# HttpConnection.java

## Přehled

Zpracovává životní cyklus jednoho TCP spojení (od požadavku po odpověď). Implementuje `SelectionConsumer`.

## Vnitřní Logika: Stavový automat

Metoda `accept()` je volána selektorem pokaždé, když je na soketu aktivita.

1. **Čtení Požadavku:** Volá `request.write(channel)`. Pokud request ještě není kompletní (čeká se na další pakety),
   metoda skončí a čeká na další probuzení selektorem.
2. **Zpracování:** Jakmile je požadavek kompletní, spustí asynchronní úlohu (`CompletableFuture`) volající
   `requestHandler.handle(request)`. To probíhá mimo vlákno serveru, aby se nezpomalovalo přijímání dalších spojení.
3. **Odesílání Odpovědi:** Po dokončení handleru začne odesílat data odpovědi (`response.read(channel)`).
4. **Keep-Alive:** Po odeslání se spojení neresetuje, ale vyčistí se stav (`request.clear()`) a čeká se na další
   požadavek ve stejném spojení.

---

# HttpRequest.java

## Přehled

Reprezentuje příchozí HTTP požadavek.

## Vnitřní Logika: Parsování streamu

- **`write(ReadableByteChannel)`**: Čte bajty z kanálu do vnitřního `ByteBuffer`.
- **Hlavičky:** Čte řádek po řádku, dokud nenarazí na prázdný řádek. Poté použije regulární výraz `REQUEST_PATTERN` k
  rozkladu prvního řádku na metodu (GET/POST), adresu a verzi protokolu.
- **Parametry:** Automaticky rozkládá Query String (např. `?world=overworld&x=10`) do mapy parametrů.

---

# HttpResponse.java

## Přehled

Reprezentuje odchozí HTTP odpověď. Podporuje streamování velkých dat a **Chunked Transfer Encoding**.

## Vnitřní Logika: Odesílání dat

- **`read(WritableByteChannel)`**: Tato metoda (název je z pohledu kanálu) zapisuje data odpovědi do soketu.
- **Chunking:** BlueMap automaticky rozděluje data do "chunks". Pro každý kus dat vypočítá jeho délku v hexadecimální
  soustavě a pošle ji před samotnými daty. To je nezbytné pro posílání dat, jejichž celkovou délku server předem nezná (
  např. dynamicky generovaný JSON).
- **Optimalizace:** Hlavičky jsou po odeslání uvolněny z paměti (`headerData = null`).

---

# HttpStatusCode.java & HttpHeader.java

- **`HttpStatusCode`**: Enum se všemi standardními HTTP kódy (200 OK, 404 Not Found atd.).
- **`HttpHeader`**: Pomocná třída pro správu HTTP hlaviček. Podporuje více hodnot v jedné hlavičce (oddělené čárkou).
