# Plugin.java

## Přehled

Rozhraní `Plugin` v BlueMap API slouží jako centrální bod pro interakci s pluginy a pro konfiguraci základních komponent
BlueMap, jako je poskytovatel skinů a továrna na ikony hráčů.

## Umístění

`de.bluecolored.bluemap.api.plugin.Plugin`

## Metody

### `getSkinProvider()`

**Popis:**
Vrací aktuálně používanou instanci `SkinProvider`, kterou BlueMap používá pro získávání skinů hráčů.

**Návratová hodnota:**

- `SkinProvider`: Instance poskytovatele skinů.

---

### `setSkinProvider(SkinProvider skinProvider)`

**Popis:**
Nastavuje nového poskytovatele skinů (`SkinProvider`), kterého bude BlueMap používat pro načítání budoucích skinů hráčů.

**Parametry:**

- `skinProvider` (`SkinProvider`): Nová instance poskytovatele skinů.

---

### `getPlayerMarkerIconFactory()`

**Popis:**
Vrací aktuálně používanou instanci `PlayerIconFactory`. Tato továrna je zodpovědná za převod obrázku skinu hráče na
ikonu (marker), která se zobrazuje na mapě.

**Návratová hodnota:**

- `PlayerIconFactory`: Instance továrny na ikony hráčů.

---

### `setPlayerMarkerIconFactory(PlayerIconFactory playerMarkerIconFactory)`

**Popis:**
Nastavuje novou továrnu na ikony hráčů (`PlayerIconFactory`).

**Parametry:**

- `playerMarkerIconFactory` (`PlayerIconFactory`): Nová instance továrny, kterou má BlueMap používat.

## Použití

Toto rozhraní umožňuje vývojářům rozšíření (addonů) nebo integrací měnit způsob, jakým BlueMap pracuje s identitou
hráčů (skiny a ikony). Například lze implementovat vlastní `SkinProvider` pro offline servery nebo vlastní
`PlayerIconFactory` pro jiný styl zobrazení hlavy hráče na mapě.
