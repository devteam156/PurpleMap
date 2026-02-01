# LenientBlockEntityArrayDeserializer.java

## Přehled

`LenientBlockEntityArrayDeserializer` je deserializér pro pole blokových entit (`BlockEntity[]`), který je tolerantní k
chybám.

## Umístění

`de.bluecolored.bluemap.core.world.mca.data.LenientBlockEntityArrayDeserializer`

## Implementovaná Rozhraní

`TypeDeserializer<BlockEntity[]>`

## Funkcionalita

- Pokud v NBT datech na místě, kde má být seznam entit, není seznam (`LIST`), deserializér to ignoruje a vrátí prázdné
  pole místo vyhození chyby.
- To je užitečné pro řešení některých anomálií v poškozených nebo modifikovaných chunk souborech.
- Pokud je tam seznam, deleguje čtení na standardní deserializér.
