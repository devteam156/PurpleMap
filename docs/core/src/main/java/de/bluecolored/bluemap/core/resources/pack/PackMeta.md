# PackMeta.java

## Přehled

`PackMeta` reprezentuje obsah souboru `pack.mcmeta`.

## Umístění

`de.bluecolored.bluemap.core.resources.pack.PackMeta`

## Vnořené třídy (Struktura JSONu)

### `Pack`

- `packFormat`: Verze formátu balíčku (číslo nebo rozsah).
- `supportedFormats`: Rozsah podporovaných formátů.
- `features`: Povolené experimentální funkce.

### `Overlay`

Definuje překryvnou vrstvu pro specifické verze formátu.

- `formats`: Rozsah verzí, pro které overlay platí.
- `directory`: Adresář s overlayem.

### `Features`

- `enabled`: Seznam povolených funkcí (Keys).
