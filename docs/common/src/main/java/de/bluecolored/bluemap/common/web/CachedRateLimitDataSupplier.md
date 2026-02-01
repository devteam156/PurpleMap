# CachedRateLimitDataSupplier.java

## Přehled

`CachedRateLimitDataSupplier` obaluje jiný `Supplier` dat a přidává cachování s časovým limitem.

## Umístění

`de.bluecolored.bluemap.common.web.CachedRateLimitDataSupplier`

## Funkcionalita

- Při zavolání `get()` zkontroluje, zda od poslední aktualizace uplynul čas `rateLimitMillis`.
- Pokud ne, vrátí cachovanou hodnotu.
- Pokud ano, zavolá delegáta, aktualizuje cache a vrátí novou hodnotu.
- Používá zámek (`ReentrantLock`) pro thread-safety, ale s `tryLock()`, takže pokud je cache právě aktualizována jiným
  vláknem, ostatní vlákna dostanou starou hodnotu (neblokují se).