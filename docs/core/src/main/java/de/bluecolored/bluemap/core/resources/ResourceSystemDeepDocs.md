# Resource Systems (Pooling & Paths)

## Přehled

Balíček `de.bluecolored.bluemap.core.resources` a jeho podbalíček `pack` spravují životní cyklus Minecraft zdrojů.
BlueMap neukládá zdroje jako prosté soubory, ale jako inteligentní objekty v poolech.

---

# ResourcePath.java (Generická třída)

## Přehled

`ResourcePath` je rozšířením třídy `Key`, které navíc může nést přímou referenci na načtený objekt (zdroj).

## Proč je to důležité?

Díky tomu mohou modely v JSONu referencovat jiné modely nebo textury pomocí cest. BlueMap nejdříve načte cesty jako
řetězce, a později (líně) do těchto objektů dosadí reálné instance `Texture` nebo `Model`.

## Vnitřní Logika

- **`getResource(supplier)`**: Líný getter. Pokud je vnitřní reference `resource` null, pokusí se objekt získat z
  předaného supplieru (obvykle `ResourcePool`) a výsledek si zapamatuje.
- **`parsePath(Path, ...)`**: Pomocná metoda pro automatické vytváření klíčů z reálných cest v souborovém systému. Např.
  převede `assets/minecraft/textures/block/stone.png` na `minecraft:block/stone`.

---

# ResourcePool.java (Generická třída)

## Přehled

Thread-safe kontejner pro zdroje určitého typu (např. všechny modely bloků).

## Atributy

- `pool`: `Map<Key, T>` - Mapování klíče na reálný objekt.
- `paths`: `Map<Key, ResourcePath<T>>` - Mapování klíče na objekt cesty.

## Vnitřní Logika a Metody

- **`put(...)`**: Přidá objekt do poolu a zároveň aktualizuje příslušný `ResourcePath`, aby na něj ukazoval.
- **`load(path, loader)`**:
    1. Zkontroluje, zda už zdroj v poolu není.
    2. Pokud ne, použije `loader` (např. JSON parser) k načtení objektu ze souboru.
    3. Výsledek uloží do poolu.
- **`load(..., mergeFunction)`**: Podporuje přepisování zdrojů (např. když novější ResourcePack upravuje existující
  model). Funkce `mergeFunction` rozhodne, jak zkombinovat stará a nová data.
- **Thread-Safety**: Všechny modifikační metody jsou `synchronized`, čtení je rychlé díky hashmapám.
