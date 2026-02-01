# ResourcesGson.java

## Přehled

`ResourcesGson` je centrální místo pro konfiguraci `Gson` instance používané pro parsování resource packů a konfigurací
v BlueMap.

## Umístění

`de.bluecolored.bluemap.core.resources.adapter.ResourcesGson`

## Konstanty

- `INSTANCE`: Předkonfigurovaná instance `Gson`.

## Metody

### `addAdapter(GsonBuilder builder)`

Přidá do `GsonBuilder`u všechny potřebné adaptéry pro BlueMap typy:

- `PostDeserializeAdapterFactory`
- `KeyAdapter`
- `AxisAdapter`, `ColorAdapter`, `DirectionAdapter`
- Vektorové adaptéry (`Vector2i`, `Vector3d`...)
- Registry adaptéry (`BlockRendererType`, `GrassColorModifier`...)
- EnumMap adaptér pro `EnumMap<Direction, Face>`
