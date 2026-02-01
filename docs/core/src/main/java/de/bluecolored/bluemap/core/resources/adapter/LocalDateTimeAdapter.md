# LocalDateTimeAdapter.java

## Přehled

`LocalDateTimeAdapter` je GSON adaptér pro `LocalDateTime`.

## Umístění

`de.bluecolored.bluemap.core.resources.adapter.LocalDateTimeAdapter`

## Dědičnost

`TypeAdapter<LocalDateTime>` -> `LocalDateTimeAdapter`

## Funkcionalita

Pro serializaci a deserializaci používá standardní formát ISO-8601 (`DateTimeFormatter.ISO_OFFSET_DATE_TIME`), např.
`2023-10-27T10:15:30+01:00`.
