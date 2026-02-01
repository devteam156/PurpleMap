# Compression Systems

## Přehled

Balíček `de.bluecolored.bluemap.core.storage.compression` poskytuje jednotné rozhraní pro různé kompresní algoritmy
používané při ukládání dlaždic a metadat.

---

# Compression.java (Rozhraní)

## Přehled

Definuje kontrakt pro kompresní algoritmy. Každá implementace ví, jak data zabalit (`compress`) a rozbalit (
`decompress`).

## Podporované Algoritmy (Registry)

- **`GZIP`**: Standardní komprese (vhodná pro web a soubory).
- **`DEFLATE`**: Rychlejší verze GZIP bez hlaviček.
- **`ZSTD`**: Moderní algoritmus s vysokým poměrem komprese i rychlostí (vyžaduje externí knihovnu).
- **`LZ4`**: Extrémně rychlá komprese s nižším poměrem.
- **`NONE`**: Žádná komprese (pouze obalení bufferem).

## Metody

- `getId()`: Identifikátor algoritmu (např. "gzip").
- `getFileSuffix()`: Přípona souboru (např. ".gz").
- `compress(OutputStream)`: Obalí výstupní stream kompresorem.
- `decompress(InputStream)`: Obalí vstupní stream dekompresorem.

---

# BufferedCompression.java

## Přehled

Standardní implementace rozhraní `Compression`, která přidává `BufferedOutputStream` a `BufferedInputStream` pro zvýšení
výkonu IO operací.

## Vnitřní Logika

Využívá funkcionální rozhraní `StreamTransformer` k mapování standardních javovských (nebo externích) streamů na
kompresní streamy.
Např. pro GZIP: `out -> new BufferedOutputStream(new GZIPOutputStream(out))`.

---

# CompressedInputStream.java

## Přehled

Speciální typ `InputStream`, který si "pamatuje", jakou metodou byl komprimován. To je klíčové pro webový server
BlueMap, který tak může poslat komprimovaná data přímo prohlížeči s příslušnou hlavičkou `Content-Encoding`, aniž by je
musel na serveru rozbalovat a znovu balit.

## Atributy

- `compression`: Instance `Compression`, která byla použita.

## Metody

- **`decompress()`**: Vrátí stream, který data za běhu rozbaluje.
- **`getCompression()`**: Vrátí použitý algoritmus.
