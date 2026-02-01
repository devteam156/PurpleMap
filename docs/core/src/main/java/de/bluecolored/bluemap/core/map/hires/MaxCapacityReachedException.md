# MaxCapacityReachedException.java

## Přehled

`MaxCapacityReachedException` je výjimka, která se vyhazuje, když `ArrayTileModel` dosáhne své maximální kapacity. To se
může stát, pokud je dlaždice extrémně složitá (obsahuje příliš mnoho geometrie) a nelze ji kompletně vyrenderovat do
jednoho modelu.

## Umístění

`de.bluecolored.bluemap.core.map.hires.MaxCapacityReachedException`

## Dědičnost

`RuntimeException` -> `MaxCapacityReachedException`
