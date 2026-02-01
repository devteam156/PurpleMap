# Live Data System

## Přehled

Balíček `de.bluecolored.bluemap.common.live` obsahuje logiku pro synchronizaci dat mezi běžícím Minecraft serverem a
webovým viewerem. Tato data se neukládají trvale (kromě situací bez webserveru), ale jsou generována za běhu.

---

# LivePlayersDataSupplier.java

## Přehled

Zodpovídá za generování seznamu online hráčů a jejich aktuální pozice, rotace a stavu.

## Vnitřní Logika a Filtrování

Metoda `get()` provádí při každém volání kontrolu všech online hráčů proti pravidlům nastaveným v `plugin.conf`:

1. **Neviditelnost:** Přeskakuje hráče v efektu neviditelnosti (pokud je zapnuto `hideInvisible`).
2. **Vanish:** Přeskakuje hráče v modu Vanish (pro módy/pluginy třetích stran).
3. **Sneaking:** Schová hráče, kteří se plíží (volitelně).
4. **Herní mód:** Filtruje hráče podle herního módu (např. SPECTATOR).
5. **Světlo:** Pokud je hráč v temné jeskyni (pod limitem `hideBelowSkyLight`), může být z mapy schován.
6. **Svět (Dimenze):** Pokud hráč není ve světě, pro který se tato mapa právě prohlíží, je označen jako `foreign` (nebo
   zcela schován).

## Struktura Výstupního JSONu

```json
{
  "players": [
    {
      "uuid": "...",
      "name": "...",
      "foreign": false,
      "position": {"x": 10, "y": 64, "z": 20},
      "rotation": {"pitch": 0, "yaw": 180, "roll": 0}
    }
  ]
}
```

---

# LiveMarkersDataSupplier.java

## Přehled

Zajišťuje serializaci markerů (značek, čar, oblastí), které byly vytvořeny pomocí API BlueMap nebo v konfiguraci mapy.

## Vnitřní Logika

Používá specializovaný `MarkerGson` z API k převodu mapy `MarkerSet`ů do JSON formátu. Tyto markery pak webový viewer
vykresluje nad 3D mapou.

- **Důležité:** Na rozdíl od hráčů, markery se obvykle mění méně často, ale tento supplier zaručuje, že jakákoli změna
  provedená přes API se okamžitě projeví všem divákům po obnovení dat v prohlížeči.
