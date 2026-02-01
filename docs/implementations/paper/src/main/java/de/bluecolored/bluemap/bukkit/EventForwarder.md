# EventForwarder.java

## Přehled

`EventForwarder` slouží k distribuci událostí o hráčích (připojení/odpojení) z Bukkit API do registrovaných
`ServerEventListener`ů BlueMap.

## Umístění

`de.bluecolored.bluemap.bukkit.EventForwarder`

## Implementovaná Rozhraní

`org.bukkit.event.Listener`

## Funkcionalita

- Naslouchá na `PlayerJoinEvent` a `PlayerQuitEvent`.
- Předává UUID hráčů všem registrovaným listenerům.
- Události mají prioritu `MONITOR` a ignorují zrušené události, aby BlueMap reagovala jen na skutečné
  připojení/odpojení.
