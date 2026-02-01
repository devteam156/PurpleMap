# Metrics.java

## Přehled

`Metrics` je třída pro odesílání anonymních statistik o používání BlueMap na server `metrics.bluecolored.de`.

## Umístění

`de.bluecolored.bluemap.common.metrics.Metrics`

## Funkcionalita

- **Odesílání reportů:** Odesílá informace o implementaci (např. "fabric", "paper"), verzi BlueMap a verzi Minecraftu.
- **Asynchronní odesílání:** Metoda `sendReportAsync` spustí odesílání v novém vlákně, aby neblokovala hlavní vlákno
  serveru.
- **Komunikace:** Používá `HttpsURLConnection` pro odeslání POST požadavku s JSON daty.

## Vnořené třídy

- `Report`: Záznam (record) reprezentující data odesílaná v reportu (implementace, verze, mcVersion).