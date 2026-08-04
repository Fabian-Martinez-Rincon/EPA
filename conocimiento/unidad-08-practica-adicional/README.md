# Unidad 8 — Práctica adicional y exámenes

Ejercitación integradora que combina todos los temas del curso (modularización, parámetros, estructuras de control), incluyendo dos enunciados de examen del año 2013.

- [ejercicios-adicionales.md](<ejercicios-adicionales.md>) — los 8 enunciados tal como aparecen en el PDF original.
- [practica-guiada.md](practica-guiada.md) — presentación alternativa de los ejercicios 1 a 3, con código resuelto y animación del recorrido.
- Figuras y animaciones: [recursos/](recursos/) (`sabado.gif` queda sin referenciar desde ningún `.md` de la unidad; no se elimina ni se inventa un uso para no tocar contenido fuera de alcance).
- Código: [codigo/](codigo/) — soluciones de los ejercicios 1 a 3 (los ejercicios 4 a 8 no tienen solución en este repositorio).

## Ejercicios atomizados (`ejercicios/` + `soluciones/`)

Los 3 ejercicios con código (1, 2 y 3) están atomizados uno por archivo en [ejercicios/](ejercicios/) y [soluciones/](soluciones/), siguiendo la misma convención que `AYP1-FABOSISTEMAS` y `unidad-02-algoritmos-y-logica`. Al verificarlos contra el enunciado y contra el intérprete de R-info de Academia-Fabo se encontraron y corrigieron 2 bugs reales en el código:

- `codigo/ejercicio-02.ri`: el driver decía `repetir 9` donde el propio comentario del archivo ("Avenidas 1 a 99") y el enunciado ("recorrer todas las avenidas") dejan claro que debía ser `repetir 99` — con el valor original el programa solo procesaba 10 de las 100 avenidas.
- `codigo/ejercicio-03.ri`: acumulaba correctamente el total de flores y papeles recogidos, pero nunca los informaba con `Informar` pese a que el enunciado lo pide explícitamente — se agregaron los dos `Informar` faltantes al final.

Cada solución quedó re-probada con el intérprete contra su `escenario_ciudad` real y contra al menos un caso límite adicional (esquina con exactamente 20/45/60 flores o papeles, borde del área 100×100); el detalle de cada corrida está documentado en la sección "Escenario de prueba" de cada `soluciones/*.md`.

**Bugs de sincronización encontrados en una segunda pasada:** `ejercicios-adicionales.md` y `practica-guiada.md` incluyen, además del enunciado, una copia embebida del código de cada solución (para lectura rápida sin ir a `codigo/`). Esas copias habían quedado desactualizadas respecto de los `.ri` reales — reproducían los mismos 2 bugs de arriba, sin el fix:

- `ejercicios-adicionales.md` (ejercicio 2) y `practica-guiada.md` (ejercicios 1 y 2): el driver embebido tenía `repetir 9` en vez de `repetir 99` (el de `practica-guiada.md` ejercicio 1 es un bug propio de esa copia — ni el `.ri` real ni `ejercicios-adicionales.md` lo tenían).
- `ejercicios-adicionales.md` y `practica-guiada.md` (ejercicio 3): el driver embebido no tenía los `Informar(totalFlores)` / `Informar(totalPapeles)` finales.

Se sincronizaron las 5 copias con el código real (ya probado) y se confirmó línea por línea, con un script de diff, que las tres copias (código real, `ejercicios-adicionales.md`, `practica-guiada.md`) coinciden ahora en lógica.

También se revisó la **descripción accesible** de la figura del ejercicio 3 (`ejercicios/ejercicio-03-...md` y `ejercicios-adicionales.md`): decía que el recorrido "aumenta progresivamente su extensión" desde (1,1), pero al trazar la ejecución real (`codigo/ejercicio-03.ri`) y comparar contra la imagen (`recursos/adicional-ejercicio-3-recorrido.png` / `recursos/enunciado.png`, y la página 1 del PDF original), la fila que arranca en (1,1) es la **más larga** (18 esquinas) y las filas siguientes se **angostan** a medida que el robot se aleja — la descripción decía lo opuesto. Se corrigió el texto en ambos archivos.

Se corrigió además un typo de concordancia en el enunciado atomizado del ejercicio 2 (`ejercicios/ejercicio-02-...md`): "la cantidad avenidas" → "la cantidad **de** avenidas" (el original en el PDF y en `ejercicios-adicionales.md`, que reproduce el PDF tal cual, mantiene la forma sin "de"; se corrigió solo en la versión atomizada pensada para lectura directa del estudiante).

De paso, probar estos archivos reveló dos vacíos reales en el intérprete de R-info (ya corregidos en `Academia-Fabo/lib/rinfo/parser.ts`): no soportaba un `proceso` declarado sin paréntesis cuando no tiene parámetros (`proceso Izquierda`, sin `()`), ni su invocación sin paréntesis (`Izquierda`, sin `()`) — ambas formas aparecen en `ejercicio-03.ri`.

## Ejercicios pendientes (sin atomizar)

Los ejercicios 4 a 8 no tienen código en este repositorio (ver nota en `ejercicios-adicionales.md`: "los ejercicios 4 a 8 no tienen solución en este repositorio") — no se atomizan para no inventar una solución sobre contenido `origen: convertido`.

**Prerrequisitos:** [unidad-07-parametros-de-entrada-salida](../unidad-07-parametros-de-entrada-salida/) (y, en general, todas las unidades anteriores).

**Exámenes voluntarios:** una variante adicional del examen (no incluida en este PDF) fue resuelta por dos estudiantes; ver [Estudiantes/](../../Estudiantes/).
