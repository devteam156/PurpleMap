# ProgressTracker.java

## Přehled

`ProgressTracker` je pomocná třída pro měření a odhadování rychlosti zpracování úloh. Slouží k výpočtu "času do konce" (
ETA) na základě reálných dat o postupu v čase.

## Umístění

`de.bluecolored.bluemap.common.rendermanager.ProgressTracker`

## Atributy

- `timer`: `java.util.Timer`, který pravidelně spouští metodu `update()`.
- `progressSupplier`: Funkce (`Supplier<Double>`), která vrací aktuální postup (0.0 až 1.0).
- `averagingCount`: Počet vzorků pro výpočet klouzavého průměru (standardně 12).
- `timesPerProgress`: Fronta (`Deque`) uchovávající vypočtené celkové časy trvání úlohy extrapolované z jednotlivých
  měření.

## Vnitřní Logika a Metody

### `update()` (Synchronizováno)

Tato metoda se spouští periodicky (standardně každých 5 sekund):

1. Získá aktuální čas a aktuální postup z `progressSupplier`.
2. Vypočítá změnu času (`deltaTime`) a změnu postupu (`deltaProgress`) od posledního měření.
3. Pokud došlo k postupu (`deltaProgress > 0`):
    - Vypočítá odhadovanou celkovou dobu trvání celé úlohy: `totalDuration = deltaTime / deltaProgress`.
    - Tuto hodnotu (v milisekundách) přidá do fronty `timesPerProgress`.
    - Pokud fronta překročí `averagingCount`, odstraní nejstarší vzorek.
    - Uloží aktuální stav pro příští měření.

### `getAverageTimePerProgress()` (Synchronizováno)

Vypočítá průměr ze všech hodnot v `timesPerProgress`. Tato hodnota v podstatě říká: "Při aktuální rychlosti by celá
úloha (od 0 do 100 %) trvala X milisekund".

### `resetAndStart(Supplier<Double> progressSupplier)`

Resetuje historii a začne měřit postup pro novou úlohu. Nastaví počáteční čas a výchozí postup.

## Použití

Využívá ho `RenderManager` k poskytování odhadu času do dokončení úlohy. ETA se pak vypočítá jako
`(1.0 - aktualni_postup) * getAverageTimePerProgress()`.
