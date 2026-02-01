# FabricPlayer.java

## Přehled

`FabricPlayer` je implementace `Player` pro Fabric. Obaluje `net.minecraft.server.network.ServerPlayerEntity`.

## Umístění

`de.bluecolored.bluemap.fabric.FabricPlayer`

## Dědičnost

`Player` -> `FabricPlayer`

## Funkcionalita

- Poskytuje informace o hráči: UUID, jméno, pozici, rotaci, herní mód, efekty (neviditelnost).
- Získává informace o světle (`skyLight`, `blockLight`) z `LightingProvider` světa.
- Metoda `update()` aktualizuje stav hráče (volána periodicky z `FabricMod`).

## Metody

Implementuje všechny metody abstraktní třídy `Player` získáváním dat z vanilla objektu hráče.
