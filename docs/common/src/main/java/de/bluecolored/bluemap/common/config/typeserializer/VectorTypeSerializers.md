# Vector2iTypeSerializer.java & Vector2dTypeSerializer.java

## Přehled

Tyto serializátory umožňují ukládat a načítat 2D vektory (celočíselné i s plovoucí čárkou) z konfiguračních souborů.

## Umístění

`de.bluecolored.bluemap.common.config.typeserializer.Vector2iTypeSerializer`
`de.bluecolored.bluemap.common.config.typeserializer.Vector2dTypeSerializer`

## Formát v konfiguraci

Vektor je reprezentován jako objekt s poli `x` a `y`.

```hocon
pos {
  x: 10
  y: 20
}
```

## Logika Deserializace

1. Získá uzly `x` a `y`.
2. **Fallback:** Pokud uzel `y` neexistuje, zkusí načíst uzel `z`. (Zajišťuje kompatibilitu se souřadnicemi v
   Minecraftu, kde horizontální rovina je často XZ).
3. Pokud `x` i `y/z` chybí, vyhodí `SerializationException`.
4. Vrátí novou instanci vektoru.

## Logika Serializace

Zapíše hodnoty do polí `x` a `y` v konfiguračním uzlu.
