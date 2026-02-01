# ResourcePack Models & Textures

## Přehled

BlueMap věrně interpretuje formát modelů a textur Minecraftu. Balíček
`de.bluecolored.bluemap.core.resources.pack.resourcepack.model` a `texture` spravuje tuto hierarchii.

---

# Model.java

## Přehled

Reprezentuje kompletní 3D model (např. blok trávy, truhla).

## Vnitřní Logika: Dědičnost a optimalizace

- **`applyParent(modelPool)`**: Implementuje rekurzivní dědičnost modelů. Pokud model nemá vlastní elementy (např.
  `stone_button`), načte je ze svého rodiče (`button`). Tato metoda také spojuje mapy textur.
- **`optimize(texturePool)`**: Převede textové názvy textur (proměnné začínající `#`) na reálné objekty `Texture`.
- **`calculateProperties(...)`**: Klíčová metoda pro výkon rendereru. BlueMap analyzuje geometrii modelu:
    - Pokud model tvoří plnou kostku (16x16x16) a všechny jeho textury jsou zcela neprůhledné, označí model jako *
      *`occluding`** a **`culling`**.
    - Renderer pak ví, že může vynechat stěny bloků pod tímto modelem.

---

# Element.java

## Přehled

Reprezentuje jednu krychli (box) v rámci modelu.

## Vnitřní Logika: UV Výpočty

- **`calculateDefaultUV(direction)`**: Pokud v JSONu chybí UV souřadnice pro danou stěnu, BlueMap je automaticky
  dopočítá na základě rozměrů elementu (`from`, `to`). Každý směr (UP, DOWN, NORTH...) má svůj specifický vzorec pro
  mapování 3D souřadnic na 2D plochu textury.
- **`isFullCube()`**: Kontroluje, zda tento element přesně odpovídá rozměrům 0-16 ve všech osách.

---

# Face.java

Reprezentuje jednu stěnu elementu.

- Obsahuje informaci o textuře, UV souřadnicích, rotaci a `tintindex`u (pro barvení biomem).
- **`cullface`**: Určuje směr, ve kterém sousední blok způsobí skrytí této stěny.

---

# Texture.java

## Přehled

Reprezentuje jeden obrázek (texturu). BlueMap ukládá textury v úsporném formátu.

## Vnitřní Logika a Data

- **Base64 Encoding**: Samotný obrázek je v paměti uložen jako Base64 string s prefixem `data:image/png;base64,...`. To
  umožňuje snadné předání do webového vieweru.
- **`color`**: Průměrná barva textury. BlueMap ji počítá automaticky při načítání (`BufferedImageUtil.averageColor`).
  Tato barva se používá pro generování lowres dlaždic.
- **`halfTransparent`**: Příznak, zda textura obsahuje poloprůhledné pixely (např. sklo vs. voda).
- **`textureImage`**: Líně načítaná reference na `BufferedImage`. Používá `SoftReference`, aby mohl Garbage Collector
  uvolnit paměť, pokud je jí nedostatek.
- **`AnimationMeta`**: Obsahuje data o animaci (pokud má textura soubor `.mcmeta`).
