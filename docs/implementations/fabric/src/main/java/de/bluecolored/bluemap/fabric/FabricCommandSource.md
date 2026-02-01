# FabricCommandSource.java

## Přehled

`FabricCommandSource` je implementace `CommandSource` pro Fabric. Obaluje
`net.minecraft.server.command.ServerCommandSource`.

## Umístění

`de.bluecolored.bluemap.fabric.FabricCommandSource`

## Implementovaná Rozhraní

`CommandSource`

## Funkcionalita

- **Odesílání zpráv:** Převádí Adventure `Component` na Minecraft `Text` pomocí JSON serializace a odesílá ho zdroji
  příkazu.
- **Oprávnění:**
    - Integruje se s Fabric Permissions API (LuckPerms atd.), pokud je dostupné.
    - Pokud není, používá vanilla systém oprávnění (level 2 - MODERATORS).
- **Poloha a Svět:** Získává pozici a svět ze `ServerCommandSource`.
