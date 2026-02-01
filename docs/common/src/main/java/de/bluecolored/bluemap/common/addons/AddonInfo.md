# AddonInfo.java

## Přehled

`AddonInfo` reprezentuje metadata addonu načtená ze souboru `bluemap.addon.json` uvnitř JAR souboru.

## Umístění

`de.bluecolored.bluemap.common.addons.AddonInfo`

## Atributy

- `id`: Unikátní ID addonu.
- `entrypoint`: Plné jméno hlavní třídy addonu (musí implementovat `Runnable`).
- `dependencies`: Seznam ID vyžadovaných addonů.
- `softDependencies`: Seznam ID volitelných addonů (pokud existují, načtou se před tímto addonem).

## Statické Metody

### `load(Path addonJarFile)`

Otevře JAR soubor, najde `bluemap.addon.json` a deserializuje ho (pomocí GSON).