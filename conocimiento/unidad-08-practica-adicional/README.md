# Unidad 8 — Práctica adicional y exámenes

Ejercitación integradora que combina todos los temas del curso (modularización, parámetros, estructuras de control), incluyendo dos enunciados de examen del año 2013.

- [ejercicios-adicionales.md](<ejercicios-adicionales.md>) — los 8 enunciados tal como aparecen en el PDF original.
- [practica-guiada.md](practica-guiada.md) — presentación alternativa de los ejercicios 1 a 3, con código resuelto y animación del recorrido.
- Fuente: [fuentes/](fuentes/).
- Figuras y animaciones: [recursos/](recursos/).
- Código: [codigo/](codigo/) — soluciones de los ejercicios 1 a 3 (los ejercicios 4 a 8 no tienen solución en este repositorio).

## Ejercicios atomizados (`ejercicios/` + `soluciones/`)

Los 3 ejercicios con código (1, 2 y 3) están atomizados uno por archivo en [ejercicios/](ejercicios/) y [soluciones/](soluciones/), siguiendo la misma convención que `AYP1-FABOSISTEMAS` y `unidad-02-algoritmos-y-logica`. Al verificarlos contra el enunciado y contra el intérprete de R-info de Academia-Fabo se encontraron y corrigieron 2 bugs reales:

- `codigo/ejercicio-02.ri`: el driver decía `repetir 9` donde el propio comentario del archivo ("Avenidas 1 a 99") y el enunciado ("recorrer todas las avenidas") dejan claro que debía ser `repetir 99` — con el valor original el programa solo procesaba 10 de las 100 avenidas.
- `codigo/ejercicio-03.ri`: acumulaba correctamente el total de flores y papeles recogidos, pero nunca los informaba con `Informar` pese a que el enunciado lo pide explícitamente — se agregaron los dos `Informar` faltantes al final.

De paso, probar estos archivos reveló dos vacíos reales en el intérprete de R-info (ya corregidos en `Academia-Fabo/lib/rinfo/parser.ts`): no soportaba un `proceso` declarado sin paréntesis cuando no tiene parámetros (`proceso Izquierda`, sin `()`), ni su invocación sin paréntesis (`Izquierda`, sin `()`) — ambas formas aparecen en `ejercicio-03.ri`.

## Ejercicios pendientes (sin atomizar)

Los ejercicios 4 a 8 no tienen código en este repositorio (ver nota en `ejercicios-adicionales.md`: "los ejercicios 4 a 8 no tienen solución en este repositorio") — no se atomizan para no inventar una solución sobre contenido `origen: convertido`.

**Prerrequisitos:** [unidad-07-parametros-de-entrada-salida](../unidad-07-parametros-de-entrada-salida/) (y, en general, todas las unidades anteriores).

**Exámenes voluntarios:** una variante adicional del examen (no incluida en este PDF) fue resuelta por dos estudiantes; ver [Estudiantes/](../../Estudiantes/).
