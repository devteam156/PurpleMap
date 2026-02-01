# MojangSkinProvider.java

## Přehled

`MojangSkinProvider` je výchozí implementace `SkinProvider`. Stahuje skiny hráčů přímo ze serverů Mojangu (Session
Server).

## Umístění

`de.bluecolored.bluemap.common.plugin.skins.MojangSkinProvider`

## Funkcionalita

1. **Získání profilu:** Pošle GET požadavek na `https://sessionserver.mojang.com/session/minecraft/profile/{UUID}`.
2. **Parsování JSON:** Z odpovědi získá pole `properties`.
3. **Dekódování textur:** Najde vlastnost `textures`, která je Base64 kódovaný JSON. Dekóduje ji.
4. **Získání URL:** V dekódovaném JSONu najde URL adresu skinu (`textures.SKIN.url`).
5. **Stažení obrázku:** Stáhne obrázek skinu z této URL.

## Ošetření chyb

Pokud se cokoli nepovede (chyba sítě, neplatné JSON, chybějící textura), metoda `load` vrátí prázdný výsledek (
`Optional.empty()`) a zaloguje chybu do debug logu.
