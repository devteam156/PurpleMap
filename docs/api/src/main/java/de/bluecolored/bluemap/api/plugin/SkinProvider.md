# SkinProvider.java

## Přehled

`SkinProvider` je funkcionální rozhraní v BlueMap API, které definuje kontrakt pro načítání skinů (vzhledů) hráčů
Minecraftu na základě jejich UUID. Toto rozhraní umožňuje BlueMap získávat obrázky skinů z různých zdrojů.

## Umístění

`de.bluecolored.bluemap.api.plugin.SkinProvider`

## Metody

### `load(UUID playerUUID)`

**Popis:**
Tato metoda se pokouší načíst skin hráče pro dané UUID.

**Parametry:**

- `playerUUID` (`UUID`): Unikátní identifikátor hráče, jehož skin se má načíst.

**Návratová hodnota:**

- `Optional<BufferedImage>`:
    - Pokud se skin podaří najít a načíst, vrací `Optional` obsahující `BufferedImage` se skinem.
    - Pokud pro dané UUID neexistuje žádný skin, vrací prázdný `Optional`.

**Výjimky:**

- `IOException`: Vyvolána, pokud dojde k chybě při pokusu o načtení skinu (např. chyba sítě, chyba čtení souboru).

## Použití

Toto rozhraní je klíčové pro systémy, které potřebují zobrazovat ikony hráčů na mapě. Implementace tohoto rozhraní může
stahovat skiny z Mojang API, z lokální cache nebo z jiných skin serverů.
