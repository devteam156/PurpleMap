# Block Systems (Access & Context)

## Přehled

Balíček `de.bluecolored.bluemap.core.world.block` definuje způsob, jakým BlueMap přistupuje k jednotlivým blokům a jakým
způsobem jim dodává kontext potřebný pro renderování (např. informace o sousedech).

---

# BlockAccess.java (Rozhraní)

## Přehled

Základní kontrakt pro jakýkoli objekt, který reprezentuje blok nebo k němu umožňuje přístup.

## Metody

- `getX(), getY(), getZ()`: Absolutní souřadnice.
- `getBlockState()`: Typ a vlastnosti bloku.
- `getLightData()`: Úroveň světla na této pozici.
- `getBiome()`: Biom na této pozici.
- `getBlockEntity()`: Doplňující data.
- `getSunLightLevel()` / `getBlockLightLevel()`: Pomocné metody pro jednotlivé složky světla.

---

# Block.java

## Přehled

Základní, lehká implementace `BlockAccess`. Je navržena jako "flyweight" objekt – jedna instance se může "posouvat" po
světě a měnit svou pozici, čímž šetří paměť.

## Atributy

- `world`: Svět, ze kterého se čtou data.
- `chunk`: Aktuálně načtený chunk (cachovaný pro zrychlení).

## Vnitřní Logika

- **`set(x, y, z)`**: Přesune objekt bloku na novou pozici.
    - **Optimalizace:** Pokud se změní jen výška Y, ale X a Z zůstávají stejné, ponechá si referenci na `chunk`, protože
      ten pokrývá celou výšku.
- **Líné načítání (Lazy Loading):** Data (stav bloku, světlo, biom) se z chunku čtou až v momentě volání příslušného
  getteru.

---

# ExtendedBlock.java

## Přehled

Dekorátor kolem `BlockAccess`, který přidává logiku specifickou pro renderování, jako jsou hranice mapy (masky), detekce
jeskyní a přístup k vlastnostem modelu.

## Atributy

- `resourcePack`: Pro získání vizuálních vlastností bloku.
- `renderSettings`: Pro kontrolu hranic a jeskyní.
- `maskArea`: Vnitřní třída spravující lokální submasku pro rychlejší testování.

## Vnitřní Logika

- **`getBlockState()`**: Pokud je blok mimo hranice renderování (`isInsideRenderBounds == false`), tváří se jako `AIR`.
  Tím se vytvářejí čisté řezy mapou.
- **`getLightData()`**: Na okrajích mapy upravuje úroveň slunečního světla pro lepší vizuální přechod.
- **`isRemoveIfCave()`**: Implementuje algoritmus pro schovávání jeskyní.
    - **Pravidlo:** Pokud je blok pod výškou Y (defaultně 55) a zároveň je pod úrovní "dna oceánu" (pokud je dostupná
      výšková mapa), je označen k odstranění.

---

# BlockNeighborhood.java

## Přehled

Speciální implementace `ExtendedBlock`, která si udržuje cache okolních bloků. Je to **klíčová třída pro renderování**,
protože každý blok potřebuje znát své sousedy pro výpočet okluze (zakrytí stěn) a míchání barev.

## Vnitřní Logika

- **Struktura:** Pole `neighborhood` o velikosti 512 prvků (8x8x8).
- **Indexace:** Používá bitovou masku `(x & 0x7) << 6 | (y & 0x7) << 3 | (z & 0x7)` pro bleskové mapování relativních
  souřadnic do pole.
- **Cachování:** Pokud je požadován soused, který ještě není v poli, vytvoří se jeho kopie a uloží se do pole. Při
  dalším požadavku na stejnou relativní pozici se vrátí již existující objekt.
