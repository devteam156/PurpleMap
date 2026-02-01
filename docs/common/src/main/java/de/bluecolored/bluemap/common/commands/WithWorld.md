# WithWorld.java

## Přehled

`WithWorld` je anotace označující příkazy, které vyžadují, aby byl `CommandSource` asociován s konkrétním světem.

## Umístění

`de.bluecolored.bluemap.common.commands.WithWorld`

## Použití

Podobně jako `WithPosition`, tato anotace slouží k filtrování použitelnosti příkazu. V `Commands.java` se ověřuje, zda
`commandSource.getWorld()` vrací existující svět a zda je tento svět známý BlueMap pluginu.
