# InterruptableReentrantLock.java

## Přehled

`InterruptableReentrantLock` je rozšíření `ReentrantLock` o speciální metodu pro získání zámku.

## Umístění

`de.bluecolored.bluemap.common.InterruptableReentrantLock`

## Dědičnost

`ReentrantLock` -> `InterruptableReentrantLock`

## Funkcionalita

- **`interruptAndLock()`**: Pokusí se získat zámek (`tryLock()`). Pokud se to nepodaří (zámek drží někdo jiný):
    1. Získá vlákno, které zámek drží (`getOwner()`).
    2. Pokud takové vlákno existuje, přeruší ho (`owner.interrupt()`).
    3. Poté standardně čeká na zámek (`lock()`).

## Použití

Tento zámek je užitečný v situacích, kdy má nová úloha vyšší prioritu než aktuálně běžící (a zámek držící) úloha a je
žádoucí tu starou "vyhodit" (např. při rychlém posunu mapy, kdy renderování starého pohledu už není potřeba).