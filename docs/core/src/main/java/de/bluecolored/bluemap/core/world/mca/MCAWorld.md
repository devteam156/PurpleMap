# MCAWorld.java

## Přehled

`MCAWorld` reprezentuje Minecraft svět uložený ve formátu MCA (Anvil).

## Umístění

`de.bluecolored.bluemap.core.world.mca.MCAWorld`

## Implementovaná Rozhraní

`World`

## Atributy

- `id`: Unikátní identifikátor světa.
- `worldFolder`: Cesta k hlavní složce světa.
- `dimension`: Identifikátor dimenze (např. `minecraft:overworld`).
- `dataPack`: DataPack asociovaný se světem.
- `levelData`: Data z `level.dat`.
- `blockChunkGrid`: Mřížka chunků s bloky (načítá se z `region/` složky).
- `entityChunkGrid`: Mřížka chunků s entitami (načítá se z `entities/` složky).

## Funkcionalita

- Načítá a poskytuje přístup k chunkům a regionům.
- Spravuje `ChunkGrid` pro bloky i entity.
- Poskytuje metody pro iteraci přes entity v určité oblasti.
- Umožňuje invalidovat cache chunků.

## Statické Metody

### `load(...)`

Načte svět ze složky. Přečte `level.dat`, zjistí nastavení dimenzí a vytvoří instanci `MCAWorld`.

### `resolveDimensionFolder(...)`

Určí cestu ke složce dimenze na základě jejího ID (řeší standardní MC strukturu `DIM-1`, `DIM1`, `dimensions/...`).