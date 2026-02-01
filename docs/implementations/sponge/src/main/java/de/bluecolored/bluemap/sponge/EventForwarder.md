# EventForwarder.java

## Přehled

`EventForwarder` je listener pro Sponge eventy, který přeposílá informace o připojení/odpojení hráčů do
`ServerEventListener`.

## Umístění

`de.bluecolored.bluemap.sponge.EventForwarder`

## Funkcionalita

- Naslouchá na `ServerSideConnectionEvent.Join` a `Leave`.
- Události mají prioritu `POST` (jsou volány až po zpracování ostatními pluginy).
- Volá metody na `listener` (což je typicky instance `BlueMap` jádra).
