# CombinedClassLoader.java

## Přehled

`CombinedClassLoader` je speciální `ClassLoader`, který deleguje hledání tříd na více rodičovských classloaderů.

## Umístění

`de.bluecolored.bluemap.common.addons.CombinedClassLoader`

## Funkcionalita

- Používá se v `AddonLoader`u k tomu, aby addon viděl třídy z BlueMap API **A ZÁROVEŇ** třídy z jiných addonů, na
  kterých závisí.
- Při volání `findClass` postupně zkouší všechny delegáty. Pokud žádný třídu nenajde, vyhodí `ClassNotFoundException`.