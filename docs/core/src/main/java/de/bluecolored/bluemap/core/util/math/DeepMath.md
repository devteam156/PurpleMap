# Color.java

## Přehled

`Color` je vysoce optimalizovaná třída pro reprezentaci a manipulaci s barvami ve formátu RGBA (plovoucí čárka).
Podporuje režim **premultiplied alpha**, který je nezbytný pro správné míchání (blending) poloprůhledných textur.

## Umístění

`de.bluecolored.bluemap.core.util.math.Color`

## Atributy

- `r, g, b, a`: `float` - Složky barvy v rozsahu 0.0 až 1.0.
- `premultiplied`: `boolean` - Příznak, zda jsou složky R, G, B již vynásobeny Alfou.

## Vnitřní Logika a Operace

### Míchání Barev (Blending)

- **`overlay(Color color)`**: Klasické míchání "vrstvy nad vrstvou".
    - **Logika:** Nová alfa se vypočítá jako `(1 - nova_alfa) * stara_alfa + nova_alfa`. Složky RGB se míchají lineárně.
      Vyžaduje, aby obě barvy byly v režimu premultiplied.
- **`underlay(Color color)`**: Vloží barvu "pod" aktuální barvu. Používá se např. při aplikaci pozadí za poloprůhledný
  blok.

### Konverze Formátů

- **`set(int color)`**: Rozloží 32bitový integer (formát ARGB) na float složky.
- **`getInt()`**: Sbalí float složky zpět do 32bitového integeru.
- **`flatten()`**: Odstraní průhlednost. Pokud je barva poloprůhledná, vypočítá výslednou neprůhlednou barvu (vydělí RGB
  složky alfou a nastaví alfu na 1.0).

### Parsování (CSS Style)

- **`parse(String value)`**: Podporuje hex kódy (např. `#ff0000`, `#f00`, `#ff0000ff`). Automaticky řeší posun Alfa
  kanálu na začátek/konec podle standardů Minecraftu a CSS.

---

# MatrixM4f.java (4x4 Matice)

## Přehled

Mutabilní 4x4 matice pro transformaci 3D souřadnic. Používá se pro rotace, škálování a posuny modelů bloků.

## Umístění

`de.bluecolored.bluemap.core.util.math.MatrixM4f`

## Klíčové Metody a Matematika

### Transformace

- **`translate(x, y, z)`**: Posune matici o daný vektor.
- **`scale(x, y, z)`**: Změní měřítko v jednotlivých osách.
- **`rotate(angle, axisX, axisY, axisZ)`**: Otočí matici kolem libovolné osy. Interně používá **Quaternions** (
  kvaterniony) pro výpočet rotace bez problému "Gimbal lock".

### Rotace XYZ / YXZ / ZYX

Specializované metody pro Eulerovy úhly (Pitch, Yaw, Roll).

- **Logika:** Výpočet probíhá přes kvaterniony:
  `qx = sx * cy * cz + cx * sy * sz` ... atd.
- Matice podporuje různé pořadí rotací, což je důležité pro správnou interpretaci rotací z Minecraft blockstate souborů.

### Násobení

- **`multiply(...)`**: Vynásobí tuto matici jinou maticí zprava.
- **`multiplyTo(...)`**: Vynásobí tuto matici jinou maticí zleva.

---

# VectorM3f.java (3D Vektor)

## Přehled

Mutabilní 3D vektor s float složkami. Navržen pro řetězení operací (Fluent API).

## Umístění

`de.bluecolored.bluemap.core.util.math.VectorM3f`

## Metody

- **`transform(MatrixM4f)`**: Nejdůležitější metoda. Aplikuje transformaci matice na tento vektor (včetně posunu).
    - **Vzorec:** `x' = m00*x + m01*y + m02*z + m03` ... atd.
- **`cross(VectorM3f)`**: Vektorový součin (výpočet normály plochy).
- **`normalize()`**: Upraví délku vektoru na 1.0.
- **`dot(VectorM3f)`**: Skalární součin (úhel mezi vektory).

---

# Axis.java (Enum)

Jednoduchý výčet os X, Y, Z.

- Obsahuje metodu `toVector()`, která vrátí jednotkový vektor dané osy (`Vector3i`).
- Používá se pro definici os rotace v konfiguračních souborech.
