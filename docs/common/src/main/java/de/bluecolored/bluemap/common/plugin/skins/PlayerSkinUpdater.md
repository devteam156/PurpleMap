# PlayerSkinUpdater.java

## Přehled

`PlayerSkinUpdater` je třída, která reaguje na připojení hráče na server a zajišťuje aktualizaci jeho skinu v úložišti
mapy. Implementuje `ServerEventListener`.

## Umístění

`de.bluecolored.bluemap.common.plugin.skins.PlayerSkinUpdater`

## Funkcionalita

- Udržuje cache časů posledních aktualizací (`skinUpdates`), aby nestahovala skiny příliš často (limit 1 hodina).
- **Asynchronní aktualizace:** Stahování a zpracování skinu probíhá v samostatném vlákně (`CompletableFuture`).
- Používá nastavený `SkinProvider` pro stažení skinu.
- Používá nastavenou `PlayerIconFactory` pro vytvoření ikony hlavy.
- Ukládá výslednou ikonu do `AssetStorage` všech načtených map pod cestou `playerheads/{UUID}.png`.
- Pokud skin není nalezen, smaže existující ikonu z úložiště.

## Metody

### `updateSkin(UUID playerUuid)`

Spustí asynchronní proces aktualizace skinu pro daného hráče.

### `onPlayerJoin(UUID playerUuid)`

Callback volaný při připojení hráče. Volá `updateSkin`.

### Gettery a Settery

Umožňuje vyměnit `SkinProvider` a `PlayerIconFactory` (využíváno API).
