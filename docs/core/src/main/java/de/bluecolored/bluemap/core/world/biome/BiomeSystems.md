# Biome Systems

## Přehled

Balíček `de.bluecolored.bluemap.core.world.biome` definuje vizuální vlastnosti prostředí, které ovlivňují barvu bloků
jako je tráva nebo listí.

---

# Biome.java (Rozhraní)

## Přehled

Definuje vizuální parametry biomu.

## Metody

- `getTemperature()` / `getDownfall()`: Používají se pro výběr barvy z colormapy (trojúhelníkový diagram teploty a
  vlhkosti).
- `getWaterColor()`: Fixní barva vody v tomto biomu.
- `getOverlay...Color()`: Barvy, které se přimíchávají k základní barvě (např. pro modované biomy).
- `getGrassColorModifier()`: Specifický efekt pro úpravu barvy trávy.

---

# GrassColorModifier.java (Enum)

## Přehled

Implementuje speciální pravidla Minecraftu pro barvu trávy v určitých biomech, která nelze vyjádřit jen teplotou.

## Implementované Modifikátory

- **`NONE`**: Nedělá nic.
- **`DARK_FOREST`**: Ztmavuje trávu.
    - **Vzorec:** `(barva + 0x28340a) >> 1` (průměr mezi barvou a tmavě zelenou).
- **`SWAMP`**: Nastavuje fixní blátivě zelenou barvu `0xff6a7039`. (Poznámka: Vanilla zde používá perlin noise, který
  BlueMap pro výkon zjednodušuje).

---

# ColorModifier.java (Rozhraní)

Jednoduchý kontrakt s metodou `apply(BlockAccess block, Color color)`, který umožňuje měnit barvu v závislosti na pozici
nebo stavu bloku.
