# MarkerGson.java

## Přehled

`MarkerGson` je pomocná třída (utility class), která poskytuje nakonfigurovanou instanci knihovny `Gson` pro serializaci
a deserializaci objektů z BlueMap API, zejména markerů a matematických typů.

## Umístění

`de.bluecolored.bluemap.api.gson.MarkerGson`

## Konstanty

### `INSTANCE`

Statická, předkonfigurovaná instance `Gson`.
Obsahuje zaregistrované adaptéry pro:

- `Marker` (a jeho podtřídy pomocí polymorfismu)
- `Line`
- `Shape`
- `Color`
- `Vector2d`, `Vector3d`, `Vector2i`, `Vector3i`

Tato instance má povolené lenient (shovívavé) parsování.

## Metody

### `addAdapters(GsonBuilder builder)`

Přidá všechny potřebné TypeAdaptery do předaného `GsonBuilder`u. Toto je užitečné, pokud si chcete vytvořit vlastní
instanci Gsonu s dalšími konfiguracemi, ale stále potřebujete podporu pro BlueMap typy.

## Interní třídy (Adaptéry)

Třída obsahuje několik vnořených statických tříd, které implementují `JsonSerializer`, `JsonDeserializer` nebo
`TypeAdapter` pro specifické typy:

- **`MarkerDeserializer`**: Rozpoznává typ markeru podle pole `"type"` v JSONu a deserializuje ho na správnou třídu (
  `HtmlMarker`, `POIMarker`, `ShapeMarker` atd.).
- **`MarkerSerializer`**: Serializuje instanci markeru podle její skutečné třídy.
- **`LineAdapter`**: Serializuje/deserializuje `Line` jako pole bodů.
- **`ShapeAdapter`**: Serializuje/deserializuje `Shape` jako pole bodů.
- **`ColorAdapter`**: Serializuje/deserializuje `Color` jako objekt s položkami `r`, `g`, `b`, `a`.
- **`VectorXdAdapter` / `VectorXiAdapter`**: Adaptéry pro vektory z knihovny `flowpowered-math`.
