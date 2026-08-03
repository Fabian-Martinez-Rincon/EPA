# Unidad 6 — Parámetros de entrada

Comunicación entre módulos mediante parámetros de entrada (`E`): declaración, uso y restricciones.

- [capitulo-6-parametros-de-entrada.md](<capitulo-6-parametros-de-entrada.md>) — teoría completa + ejercitación.
- Fuente: [fuentes/](fuentes/).
- Figuras: [recursos/](recursos/) (Top-Down, recorridos de cuadrados/rectángulos/escalones).
- Código:
  - [codigo/ejemplos/parametros-entrada](codigo/ejemplos/parametros-entrada/) — comparar procesos sin parámetros con sus versiones parametrizadas; corresponden a los Ejemplos 6.1-6.3 del capítulo (no a la ejercitación numerada), por eso no están atomizados como ejercicios.
  - [codigo/soluciones/capitulo-06](codigo/soluciones/capitulo-06/).
  - [codigo/archivo-historico/duplicado-capitulo-06](codigo/archivo-historico/duplicado-capitulo-06/) — copia antigua de estas mismas soluciones, que en algún momento había quedado clasificada como capítulo 1. Se conserva para no perder información; la versión de referencia es `codigo/soluciones/capitulo-06`.

## Ejercicios atomizados (`ejercicios/` + `soluciones/`)

Los 8 ejercicios de la "Ejercitación" del capítulo ya están atomizados uno por archivo, con front matter YAML y solución explicada (análisis, estrategia, casos límite, errores frecuentes) en [ejercicios/](ejercicios/) y [soluciones/](soluciones/). A diferencia de unidad-02, en esta unidad la correspondencia ejercicio↔código no requirió inferencia: cada archivo bajo `codigo/soluciones/capitulo-06/` ya trae en su primera línea un comentario `{Ejercitación, ejercicio N: ...}` con el enunciado exacto, y el propio capítulo incluye una tabla ("Código relacionado con la ejercitación") que mapea cada ejercicio a sus archivos. Varios ejercicios (2, 4, 5 y 6) tienen más de un archivo de código porque el enunciado pide resolver varios recorridos o sub-partes con el mismo proceso; en esos casos la solución atomizada documenta cada variante por separado bajo el mismo número de ejercicio.

Todo el código atomizado fue probado con el intérprete de R-info de `Academia-Fabo` (parseo + ejecución de punta a punta, sin excepciones inesperadas).

Durante esta atomización se encontró y corrigió 1 bug puntual:

- `codigo/soluciones/capitulo-06/Cap6_Preg_8`: el proceso `Avenida` asignaba un valor al parámetro de entrada `pasos` (`pasos:=noventa`) para acotarlo a 99 — justo la infracción que la sección 6.5 del capítulo ("Restricción en el uso de los parámetros de entrada") explica con su propio ejemplo corregido (`UnaMenosV1` → `UnaMenosV2`). Se aplicó la misma corrección del capítulo: se agregó una variable local (`pasosReales`), se copió `pasos` en ella al entrar al proceso, y el resto de la lógica pasó a operar sobre esa variable local. El comportamiento numérico no cambia (el intérprete de Academia-Fabo no impedía la asignación original), pero el código ya no viola la restricción que el propio capítulo enseña.

Ver el detalle completo en `soluciones/ejercicio-08-avenida-con-tope-de-99-pasos.md`, sección "Corrección aplicada durante esta organización".

### Observaciones documentadas sin corregir (no son bugs de una palabra)

- **Ejercicio 6 (b, c y d)** — `Cap6_Preg_6B/6C/6D`: las tres variantes que encadenan varias avenidas (todas, 5 a 15, y las pares) alcanzan la última avenida pedida pero no llegan a recorrerla (falta una vuelta más de `repetir` en cada caso: 99→100, 10→11, 49→50). Se documenta en `soluciones/ejercicio-06-recorrer-avenidas-con-numero-parametrizado.md` ("Alcance no corregido") en vez de corregirse, porque el mismo patrón se repite igual en las tres variantes — no es un error de una palabra suelta sino una cuestión de cómo se calculó el límite del `repetir` en el material original (mismo criterio ya usado en unidad-02 para el ejercicio 9). Por este motivo esa solución quedó con `estado: "parcial"`.
- **Ejercicio 6 (las cuatro partes)** — el proceso `JuntarFlor` recibe un parámetro `NumFlores` y declara variables para contar flores, pero nunca llega a consultar `HayFlorEnLaEsquina` ni a levantar nada: solo recorre avenidas. No es un bug contra el enunciado (que en las cuatro partes solo pide "recorrer", no juntar flores), pero sí evidencia de que el proceso se copió de otro ejercicio de la ejercitación sin adaptarlo del todo. Documentado en la misma solución.
- **Ejercicio 5, variantes B y C** — `Cap6_Preg_5B` y `Cap6_Preg_5C` tienen exactamente el mismo código (solo cambia el comentario de encabezado), aunque la figura 6.7 muestra cuatro recorridos visualmente distintos. Es probable que la variante C debiera ser diferente en el material original y haya quedado duplicada por error. No se intentó reconstruir una variante C distinta por falta de evidencia de cuál sería el recorrido correcto — documentado en `soluciones/ejercicio-05-recorridos-en-escalones-con-parametros.md`.

**Prerrequisitos:** [unidad-05-programacion-estructurada](../unidad-05-programacion-estructurada/).

**Siguiente unidad:** [unidad-07-parametros-de-entrada-salida](../unidad-07-parametros-de-entrada-salida/).
