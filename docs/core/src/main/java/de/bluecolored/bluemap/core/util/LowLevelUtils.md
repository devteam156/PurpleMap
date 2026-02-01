# InstancePool.java (Generická třída)

## Přehled

`InstancePool` je implementace vzoru **Object Pool**. Slouží k recyklaci drahých objektů, čímž drasticky snižuje zátěž
Garbage Collectoru v kritických částech kódu (zejména při renderování hires modelů).

## Umístění

`de.bluecolored.bluemap.core.util.InstancePool`

## Atributy

- `creator`: `Supplier<T>` - Funkce pro vytvoření nové instance, pokud je pool prázdný.
- `recycler`: `Function<T, T>` - Funkce pro vyčištění/resetování instance před jejím vrácením do poolu.
- `pool`: `ConcurrentLinkedQueue<T>` - Vláknově bezpečná fronta dostupných instancí.
- `autoClearTime`: `Duration` - Čas, po kterém se pool automaticky vyprázdní, pokud není používán.

## Vnitřní Logika a Metody

### `claimInstance()`

- **Logika:** Pokusí se vyjmout instanci z fronty (`pool.poll()`). Pokud tam žádná není, vytvoří novou pomocí `creator`.
  Resetuje časovač automatického vyčištění.

### `recycleInstance(T instance)`

- **Logika:** Přijme použitou instanci, prožene ji přes `recycler` (který ji např. vynuluje) a pokud výsledek není null,
  vrátí ji do fronty (`pool.offer`).

### `updateAutoClear()` (Synchronizováno)

- **Logika:** Pokud je nastaven `autoClearTime`, naplánuje úlohu v `AutoClearTimer`, která po uplynutí doby zavolá
  `clear()`. Každý claim/recycle tento časovač posouvá. Tím se zajistí, že pool nezabírá paměť, když se zrovna
  nerenderuje.

---

# BufferedImageUtil.java

## Přehled

Nízkoúrovňové utility pro práci s `BufferedImage`, které obcházejí některé pomalé části nebo chyby v standardním Java
AWT.

## Umístění

`de.bluecolored.bluemap.core.util.BufferedImageUtil`

## Klíčové Metody

### `halfTransparent(BufferedImage)`

- **Účel:** Zjistí, zda obrázek obsahuje poloprůhledné pixely (alfa kanál mezi 0 a 1).
- **Logika:** Prochází obrázek pixel po pixelu. Pokud najde alespoň jeden takový pixel, okamžitě vrací `true`.

### `averageColor(BufferedImage)`

- **Účel:** Vypočítá průměrnou barvu celého obrázku. Používá se pro generování barev pro nízkorozlišené dlaždice (
  lowres).
- **Logika:** Sečte barvy všech pixelů (v režimu premultiplied alpha) a vydělí je počtem pixelů.

### `readPixel(...)`

- **Logika:** Obsahuje **Workaround pro Java bug 5051418**. Pro standardní typy obrázků používá `image.getRGB()`, ale
  pro šedotónové nebo vlastní typy čte data přímo z `Raster`u (`image.getData().getPixel()`), aby předešla zkreslení
  barev.

---

# Direction.java (Enum)

## Přehled

Definuje 6 základních směrů v 3D prostoru Minecraftu.

## Atributy

- `dir`: `Vector3i` - Jednotkový vektor směru (např. UP = 0, 1, 0).
- `axis`: `Axis` - Osa, ve které směr leží (X, Y, Z).
- `opposite`: Opačný směr.
- `left` / `right`: Směry otočené o 90 stupňů v horizontální rovině.
- `localUp`: Směr, který se považuje za "nahoru" z pohledu daného směru (používá se pro rotaci textur).

---

# File Tree Iteration (NIO Extensions)

BlueMap obsahuje vlastní implementaci procházení souborů, protože standardní `Files.walk` je v některých situacích
příliš striktní.

### `FileTreeWalker.java`

- Kopie standardního `java.nio.file.FileTreeWalker`, která je ale upravena tak, aby byla přístupná pro
  `FileTreeIterator`.
- Spravuje zásobník (`stack`) otevřených adresářů.

### `FileTreeIterator.java`

- **Klíčová vlastnost:** Ignoruje `NoSuchFileException`.
- **Proč?**: Pokud BlueMap prochází miliony souborů s dlaždicemi a mezitím jiný proces (nebo vlákno) nějakou dlaždici
  smaže, standardní Java iterátor by havaroval. Tato verze prostě pokračuje dál.

---

# Cesty a Návštěvníci (Visitors)

### `DeletingPathVisitor.java`

- Implementuje rekurzivní mazání. Nejdříve smaže soubory v adresáři a v metodě `postVisitDirectory` smaže samotný (nyní
  již prázdný) adresář.

### `CopyingPathVisitor.java`

- Implementuje rekurzivní kopírování.
- **Logika:** Automaticky vytváří cílové adresáře (`preVisitDirectory`) a kopíruje soubory s volitelnými `CopyOption`.
- Používá `relativize` a `resolve` pro zachování struktury složek mezi zdrojem a cílem.
