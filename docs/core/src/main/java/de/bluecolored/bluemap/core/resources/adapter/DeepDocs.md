# Resource Serialization (GSON)

## Přehled

Balíček `de.bluecolored.bluemap.core.resources.adapter` definuje, jak se převádějí JSON data z Minecraft ResourcePacků
na vnitřní Java objekty BlueMap.

---

# ResourcesGson.java

## Přehled

Centrální konfigurátor Gson builderu. Registruje všechny potřebné adaptéry pro parsování modelů, textur a stavů bloků.

## Klíčové Registrace

- **Vektory:** Adaptéry pro `Vector2i`, `Vector3f`, `Vector4f` atd. Umožňují parsovat pole čísel v JSON jako matematické
  vektory.
- **Klíče:** `KeyAdapter` převádí řetězce (např. "minecraft:stone") na objekty `Key`.
- **Barvy:** `ColorAdapter` rozumí hex kódům i polím s RGBA hodnotami.
- **Registry:** Používá generický `RegistryAdapter` pro automatické vyhledávání typů v registrech BlueMap (např.
  `GrassColorModifier`).
- **`PostDeserializeAdapterFactory`**: Speciální továrna, která po načtení jakéhokoli objektu zkontroluje, zda
  implementuje rozhraní `PostDeserializable`, a pokud ano, zavolí jeho metodu `postDeserialize()`. To se používá pro
  dodatečnou validaci nebo inicializaci polí, která nelze vyjádřit čistě v JSONu.

---

# PostDeserializeAdapterFactory.java

## Přehled

Implementuje vzor "Post-Processing" pro Gson.

## Vnitřní Logika

1. **Intercept:** Zachytí pokus o vytvoření adaptéru pro libovolnou třídu.
2. **Proxy:** Obalí standardní adaptér.
3. **Čtení:** Nejdříve nechá standardní adaptér načíst objekt z JSONu.
4. **Akce:** Pokud výsledný objekt implementuje `PostDeserializable`, okamžitě zavolá jeho metodu. Tím BlueMap zajišťuje
   integritu dat (např. přepočet relativních cest na absolutní) hned po načtení.

---

# KeyAdapter.java

- **Logika:** Čte JSON string. Pokud obsahuje dvojtečku, rozdělí ji na namespace a hodnotu. Pokud ne, použije výchozí
  namespace. Zajišťuje, aby všechny klíče v modelech byly konzistentní.

---

# EnumMapInstanceCreator.java

- **Proč?**: GSON má občas problém s automatickým vytvořením `EnumMap`. BlueMap používá tento creator, aby zajistila, že
  mapy směrů (`Direction -> Face`) budou vytvořeny efektivně jako `EnumMap` místo obecné `HashMap`.
