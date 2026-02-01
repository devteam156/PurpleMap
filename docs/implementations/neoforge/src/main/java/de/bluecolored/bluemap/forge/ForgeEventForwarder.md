# ForgeEventForwarder.java

## Přehled

`ForgeEventForwarder` slouží k distribuci událostí o hráčích (připojení/odpojení) registrovaným listenerům BlueMap v
prostředí NeoForge.

## Umístění

`de.bluecolored.bluemap.forge.ForgeEventForwarder`

## Funkcionalita

- Obsahuje metody anotované `@SubscribeEvent` pro `PlayerLoggedInEvent` a `PlayerLoggedOutEvent` (z balíčku
  `net.neoforged`).
- Předává tyto události všem registrovaným `ServerEventListener`ům.
