# EventForwarder.java

## Přehled

`EventForwarder` slouží k distribuci událostí o hráčích (připojení/odpojení) z Bukkit API do registrovaných
`ServerEventListener`ů BlueMap.

## Umístění

`de.bluecolored.bluemap.bukkit.EventForwarder`

## Implementovaná Rozhraní

`Listener`

## Funkcionalita

- Naslouchá na `PlayerJoinEvent` a `PlayerQuitEvent`.
- Události mají prioritu `MONITOR` a ignorují zrušené události.
- Předává UUID hráčů všem registrovaným listenerům.
