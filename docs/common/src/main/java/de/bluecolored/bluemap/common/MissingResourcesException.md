# MissingResourcesException.java

## Přehled

`MissingResourcesException` je výjimka vyhozená v případě, že BlueMap chybí kritické zdroje (např. stažený Minecraft
klient jar) a není povoleno automatické stažení.

## Umístění

`de.bluecolored.bluemap.common.MissingResourcesException`

## Dědičnost

`ConfigurationException` -> `MissingResourcesException`

## Význam

Indikuje, že uživatel musí v konfiguraci povolit stahování souborů (`accept-download: true`) nebo je dodat ručně, jinak
plugin nemůže fungovat.