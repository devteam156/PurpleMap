# LegacyBiomes.java

## Přehled

`LegacyBiomes` slouží k mapování starých číselných ID biomů (používaných před 1.13) na moderní textové identifikátory (
Keys).

## Umístění

`de.bluecolored.bluemap.core.world.mca.chunk.LegacyBiomes`

## Funkcionalita

- Obsahuje statické pole `BIOME_KEYS`, které mapuje ID (0-255) na `Key` (např. 1 -> `minecraft:plains`).
- Při inicializaci načte instance `Biome` z `DataPack`u pro tato ID.

## Metody

### `forId(int legacyId)`

Vrátí objekt `Biome` odpovídající starému ID.
