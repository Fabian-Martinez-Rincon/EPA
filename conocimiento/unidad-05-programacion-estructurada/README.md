# Unidad 5 — Programación estructurada

Descomposición Top-Down, programación modular (procesos), independencia y reusabilidad de módulos.

- [capitulo-5-programacion-estructurada.md](<capitulo-5-programacion-estructurada.md>) — teoría completa + ejercitación.
- Fuente: [fuentes/](fuentes/).
- Figuras: [recursos/](recursos/) (diagramas Top-Down y recorridos).
- Código:
  - [codigo/ejemplos/modularizacion](codigo/ejemplos/modularizacion/) — programas breves para estudiar la modularización antes de resolver la ejercitación completa.
  - [codigo/soluciones/capitulo-05](codigo/soluciones/capitulo-05/).

## Ejercicios atomizados (`ejercicios/` + `soluciones/`)

De los 11 ejercicios de la sección "Ejercitación" del capítulo, 4 tienen código identificado con evidencia suficiente (comentario `{...}` propio del archivo coincidente con el enunciado) y ya están atomizados uno por archivo, con front matter YAML y solución explicada (análisis, estrategia, casos límite, errores frecuentes) en [ejercicios/](ejercicios/) y [soluciones/](soluciones/): ejercicios **1, 2, 3 y 4**. A diferencia de unidad-02, esta unidad no usa procesos con parámetros `E`/`ES` — los 11 ejercicios de la ejercitación (y toda la teoría del capítulo) trabajan exclusivamente con procesos sin parámetros; los parámetros de entrada son el tema de la [unidad 6](../unidad-06-parametros-de-entrada/), no de esta.

Durante esta atomización se revisó el código de cada uno contra su propio enunciado (mismo estándar que en unidad-02) y se encontró y corrigió 1 bug puntual heredado del material histórico:

- `codigo/soluciones/capitulo-05/Cap5_1`, `Cap5_2A` y `Cap5_2B`: el proceso `cuadrado` usaba `repetir 3` (cuadrado de lado 3) en vez de `repetir 2`, en contradicción con el enunciado del ejercicio 1 ("cuadrado de lado 2"), con el propio comentario del archivo y con el módulo `cuadrado` de lado 2 que la teoría del capítulo define en el Ejemplo 5.6. Se corrigió a `repetir 2` en los tres archivos (y, por consistencia, también en la copia sin uso de ese mismo proceso que quedaba como código muerto en `Cap5_3`, `Cap5_4A`, `Cap5_4B`, `Cap5_4C` y `Cap5_4C otro` — verificado con el intérprete que no cambia el comportamiento de esos cinco archivos). Los bloques de código embebidos en `capitulo-5-programacion-estructurada.md` se actualizaron para reflejar la misma corrección.

Cada corrección está documentada en detalle en la solución correspondiente, bajo "Corrección aplicada durante esta organización". Además, la solución del ejercicio 3 documenta (sin corregir, por ser un cambio estructural y no un fix de una palabra) que al proceso `rectangulo` de `Cap5_3` le falta el giro final que sí tienen sus copias reutilizadas en el ejercicio 4; y la solución del ejercicio 2 documenta que no se pudo confirmar con certeza la correspondencia exacta entre las variantes de código (A/B) y las sub-figuras a)/b) de la figura 5.9, a partir de la imagen escaneada del material original.

Se probaron los 8 archivos de código atomizados (Cap5_1, Cap5_2A, Cap5_2B, Cap5_3, Cap5_4A, Cap5_4B, Cap5_4C, Cap5_4C otro) contra el intérprete de R-info de Academia-Fabo: todos parsean y ejecutan sin errores.

## Ejercicios pendientes (sin atomizar)

- **Ejercicios 5, 6, 7, 9, 10 y 11**: no tienen código identificado con evidencia suficiente; no se atomizan para no inventar contenido.
- **Ejercicio 8** (`codigo/soluciones/capitulo-05/Cap 5_8`): el enunciado pide recorrer la avenida 1 juntando flores, la calle 1 juntando papeles, y así con las avenidas/calles siguientes — pero los procesos `recorrerAvenida`/`recorrerCalle` del archivo histórico no juntan ni depositan ningún elemento (no invocan `tomarFlor`/`tomarPapel` en ningún lado, ni existe un proceso que lo haga). Además, cada uno de esos procesos termina con un `Pos(1,1)` que descarta cualquier avance logrado. Probado contra el intérprete, el programa además corta con un error de "se salió de la ciudad" en la segunda vuelta del bucle principal (`repetir 99`), porque el desplazamiento acumulado (`Pos(PosAv+avenidas,PosCa+calles)`) crece cada vuelta y el recorrido de 99 esquinas desde una posición ya desplazada excede el área de 100x100. Son varios problemas entrelazados (falta la lógica central del enunciado, más un error de límites), no un fix quirúrgico; queda pendiente de una reescritura futura.
- **`codigo/soluciones/capitulo-05/Cap5Ejempo4`**: no corresponde a ninguno de los 11 enunciados numerados de la ejercitación (su código reproduce el Ejemplo 5.4 de la teoría, no un ejercicio); ya estaba marcado como `requiere_revision` en `capitulo-5-programacion-estructurada.md` y se mantiene así, sin atomizar.
- **`codigo/ejemplos/modularizacion/*.ri`** (6 archivos): son material de apoyo para ilustrar la motivación de la modularización (código sin procesos vs. con procesos, recolectando flores en cuadrados de lado 10), sin enunciado numerado propio en el capítulo — ya identificados así en el comentario `{...}` de cada archivo. No se atomizan como ejercicios.

**Prerrequisitos:** [unidad-04-repaso](../unidad-04-repaso/).

**Siguiente unidad:** [unidad-06-parametros-de-entrada](../unidad-06-parametros-de-entrada/).
