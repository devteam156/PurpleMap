# FabricEventForwarder.java

## Přehled

`FabricEventForwarder` slouží k distribuci událostí ze serveru (Fabric API) do registrovaných `ServerEventListener`ů v
BlueMap.

## Umístění

`de.bluecolored.bluemap.fabric.FabricEventForwarder`

## Funkcionalita

- Registruje se na Fabric eventy `ServerPlayConnectionEvents.JOIN` a `DISCONNECT`.
- Udržuje kolekci listenerů.
- Při vyvolání eventu projde listenery a zavolá příslušnou metodu (`onPlayerJoin`, `onPlayerLeave`).
