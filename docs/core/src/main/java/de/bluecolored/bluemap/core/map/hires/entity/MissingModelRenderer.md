# MissingModelRenderer.java (Entity)

## Přehled

`MissingModelRenderer` pro entity je záložní renderer, který se použije, když pro danou entitu není v resource packu
nalezena definice.

## Umístění

`de.bluecolored.bluemap.core.map.hires.entity.MissingModelRenderer`

## Implementovaná Rozhraní

`EntityRenderer`

## Funkcionalita

- Podobně jako u bloků, snaží se najít fallback renderer v registru.
- Pokud nic nenajde, použije `DEFAULT`, což obvykle nic nevykreslí (entity prostě zmizí), nebo vykreslí "chybějící"
  model, pokud je tak definován.
