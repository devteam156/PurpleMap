# WebserverConfig.java

## Přehled

`WebserverConfig` konfiguruje vestavěný HTTP server v BlueMap. Odpovídá souboru `webserver.conf`.

## Umístění

`de.bluecolored.bluemap.common.config.WebserverConfig`

## Atributy

### Síťové nastavení

- `enabled`: Zda má BlueMap spustit vlastní webserver.
- `ip`: Adresa, na které má server naslouchat.
    - `0.0.0.0` nebo `::0`: Všechna rozhraní.
    - `#getLocalHost`: Pokusí se zjistit lokální IP.
- `port`: TCP port (výchozí 8100).

### Soubory

- `webroot`: Adresář, ze kterého server poskytuje soubory (musí se shodovat s `WebappConfig`).

### Logování

- `log`: Konfigurace přístupového logu (`LogConfig`).
    - `file`: Soubor pro logy webserveru.
    - `append`: Režim zápisu.
    - `format`: Formátovací řetězec logu (printf styl).

## Metody

### `resolveIp()`

- **Logika:** Převede textovou konfiguraci `ip` na instanci `java.net.InetAddress`. Řeší speciální případy jako "všechna
  rozhraní" nebo "localhost".