# CombinedMask.java

## Přehled

`CombinedMask` umožňuje skládat více masek dohromady. Podporuje aditivní (sjednocení) i subtraktivní (rozdíl) operace.

## Umístění

`de.bluecolored.bluemap.core.map.mask.CombinedMask`

## Funkcionalita

- Udržuje seznam vrstev (`MaskLayer`), kde každá vrstva obsahuje masku a boolean hodnotu (`true` = přidat, `false` =
  odečíst).
- Při testování bodu prochází vrstvy **odzadu** (od poslední přidané k první). První maska, která bod "zachytí" (
  obsahuje ho), určí výsledek podle své hodnoty.
- Pokud žádná maska bod nezachytí, výsledek je `false` (mimo masku), pokud seznam vrstev není prázdný.

## Metody

### `add(Mask mask, boolean value)`

Přidá masku do seznamu.

- `value`: `true` pro oblast, která se má renderovat, `false` pro oblast, která se má vynechat (díra).

### `test(...)`

Implementuje logiku skládání masek.

### `submask(...)`

Vrátí optimalizovanou masku pro danou podoblast (odstraní vrstvy, které jsou v dané oblasti irelevantní).
