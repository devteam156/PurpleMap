# Face.java

## Přehled

`Face` definuje jednu stěnu elementu. Obsahuje informace o textuře, UV souřadnicích a dalších vlastnostech.

## Umístění

`de.bluecolored.bluemap.core.resources.pack.resourcepack.model.Face`

## Atributy (z JSONu)

- `uv`: UV souřadnice na textuře (`Vector4f` - x1, y1, x2, y2).
- `texture`: Odkaz na texturu (`TextureVariable`).
- `cullface`: Směr, ve kterém se má kontrolovat sousední blok pro culling (skrývání stěny).
- `rotation`: Rotace textury (0, 90, 180, 270).
- `tintindex`: Index barvy (pro biome-blend nebo barvení lektvary). -1 znamená bez barvení.

## Metody

### `init(...)`

Pokud UV souřadnice nejsou v JSONu zadány, vypočítá je automaticky z pozice stěny (výchozí Minecraft chování).
