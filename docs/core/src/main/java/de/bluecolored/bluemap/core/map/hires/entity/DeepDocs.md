# Entity Rendering System

## Přehled

Balíček `de.bluecolored.bluemap.core.map.hires.entity` zodpovídá za začlenění 3D objektů, které technicky nejsou bloky (
podle Minecraftu), do hires modelu mapy. Typickými příklady jsou truhly, vlajky nebo hlavy hráčů.

---

# EntityRenderPass.java

## Přehled

Průchod rendereru, který do modelu doplňuje entity.

## Vnitřní Logika

1. **Iterace:** Prochází oblast dlaždice voláním `world.iterateEntities(...)`.
2. **Kontext:** Pro každou entitu nastaví virtuální `BlockNeighborhood` na pozici, kde entita stojí. To je nutné pro
   výpočet okolního světla.
3. **Renderování:** Zavolá `entityRenderer.render(...)`.
4. **Transformace:** Po vygenerování geometrie modelu entity ji renderer automaticky posune (`translate`) na přesnou
   pozici entity ve světě (včetně desetinných míst, na rozdíl od bloků).

---

# EntityModelRenderer.java

## Přehled

Zpracovává "stav entity" a převádí ho na geometrii.

## Vnitřní Logika

- **EntityState:** Vyhledá v ResourcePacku definici stavu pro dané ID entity.
- **Části (Parts):** Entity se v BlueMap (i v Minecraftu) skládají z částí. Renderer projde všechny části, pro každou
  vybere správný renderer (např. `ResourceModelRenderer`) a vygeneruje její trojúhelníky.
- **Rotace:** Po vyrenderování všech částí aplikuje na celou entitu rotaci (YXZ) odpovídající pohledu entity ve hře (
  Yaw/Pitch).

---

# ResourceModelRenderer.java (Entity Verze)

## Přehled

Podobně jako u bloků, tento renderer interpretuje JSON modely, ale s několika úpravami pro entity.

## Klíčové Rozdíly oproti Block verzi

- **Měřítko:** Používá konstantu `SCALE = 1/16`, protože modely v JSON jsou v jednotkách 0-16, ale ve světě musí
  odpovídat velikosti 1 bloku.
- **Ambient Occlusion:** U entit je AO standardně vypnuto (nastaveno na 1.0), protože entity jsou často uprostřed bloku
  a okolní AO by na nich vypadalo nepřirozeně.
- **Tinting:** Používá rozhraní `TintColorProvider`. To umožňuje dynamicky barvit části entity (např. barva kůže u skinu
  hlavy).
- **Světlo:** Úroveň světla se bere z pozice "nohou" entity.

---

# EntityRenderer.java (Rozhraní)

Definuje kontrakt pro renderery jednotlivých částí entit. Metoda `render` přijímá:

- `Entity`: Data o entitě.
- `BlockNeighborhood`: Informace o okolí (světlo).
- `Part`: Konkrétní část modelu k vykreslení.
- `TileModelView`: Cílový model.
