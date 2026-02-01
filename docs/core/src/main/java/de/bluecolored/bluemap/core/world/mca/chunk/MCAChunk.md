# MCAChunk.java (Abstraktní základ)

## Přehled

`MCAChunk` je společný předek pro všechny implementace chunků načtených z formátu MCA (Anvil). Definuje základní
konstanty a společná data, jako je verze dat a vazba na svět.

## Umístění

`de.bluecolored.bluemap.core.world.mca.chunk.MCAChunk`

## Balíček

`de.bluecolored.bluemap.core.world.mca.chunk`

## Konstanty

- `BLOCKS_PER_SECTION`: 4096 (16x16x16) - počet bloků v jedné sekci chunku.
- `BIOMES_PER_SECTION`: 64 (4x4x4) - počet vzorků biomů v sekci (pro moderní verze).
- `VALUES_PER_HEIGHTMAP`: 256 (16x16) - počet hodnot v polích výškových map.

## Atributy

- `world`: `MCAWorld` - svět, ke kterému chunk patří.
- `dataVersion`: `int` - číselná verze formátu dat (DataVersion z NBT).

## Vnořené třídy

- `Data`: Jednoduché DTO pro základní deserializaci hlavičky chunku pomocí BlueNBT. Obsahuje pouze `dataVersion`.