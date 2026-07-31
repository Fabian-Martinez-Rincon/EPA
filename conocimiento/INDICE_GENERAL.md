# Índice general — EPA (Expresión de Problemas y Algoritmos)

Catálogo de toda la base de conocimiento convertida a Markdown, pensado para recuperación humana y por IA. Cada fila enlaza el archivo canónico; el front matter YAML de cada archivo contiene el detalle completo (`id`, `subtemas`, `fuentes`, `prerrequisitos`, `relacionados`, `codigo_relacionado`).

## Por unidad y orden recomendado

| Unidad | Tema | Archivo | Nivel | Tipo | Fuente (PDF) | Prerrequisitos |
|---:|---|---|---|---|---|---|
| 0 | Presentación del curso | [unidad-00-introduccion/00-caratula.md](unidad-00-introduccion/00-caratula.md) | inicial | resumen | [PDF](<unidad-00-introduccion/fuentes/00-Caratula.pdf>) | — |
| 0 | Introducción al curso | [unidad-00-introduccion/capitulo-0-introduccion.md](unidad-00-introduccion/capitulo-0-introduccion.md) | inicial | teoria | [PDF](<unidad-00-introduccion/fuentes/Capitulo 0-Introduccion.pdf>) | CON-EPA-U00-CARATULA |
| 1 | Resolución de problemas | [unidad-01-resolucion-de-problemas/capitulo-1-resolucion-de-problemas.md](<unidad-01-resolucion-de-problemas/capitulo-1-resolucion-de-problemas.md>) | inicial | teoria | [PDF](<unidad-01-resolucion-de-problemas/fuentes/Capitulo 1-Resolucion de problemas.pdf>) | CON-EPA-U00-INTRODUCCION |
| 2 | Algoritmos, lógica y R-info | [unidad-02-algoritmos-y-logica/capitulo-2-algoritmos-y-logica.md](<unidad-02-algoritmos-y-logica/capitulo-2-algoritmos-y-logica.md>) | inicial | teoria | [PDF](<unidad-02-algoritmos-y-logica/fuentes/Capitulo 2-Algoritmos y Logica.pdf>) | CON-EPA-U01-RESOLUCION-PROBLEMAS |
| 3 | Datos y variables | [unidad-03-datos/capitulo-3-datos.md](unidad-03-datos/capitulo-3-datos.md) | inicial | teoria | [PDF](<unidad-03-datos/fuentes/Capitulo 3-Datos.pdf>) | CON-EPA-U02-ALGORITMOS-LOGICA |
| 4 | Repaso integrador | [unidad-04-repaso/capitulo-4-repaso.md](unidad-04-repaso/capitulo-4-repaso.md) | inicial | teoria | [PDF](<unidad-04-repaso/fuentes/Capitulo 4-Repaso.pdf>) | CON-EPA-U03-DATOS |
| 5 | Programación estructurada | [unidad-05-programacion-estructurada/capitulo-5-programacion-estructurada.md](<unidad-05-programacion-estructurada/capitulo-5-programacion-estructurada.md>) | inicial | teoria | [PDF](<unidad-05-programacion-estructurada/fuentes/Capitulo 5-Programacion Estructurada.pdf>) | CON-EPA-U04-REPASO |
| 6 | Parámetros de entrada | [unidad-06-parametros-de-entrada/capitulo-6-parametros-de-entrada.md](<unidad-06-parametros-de-entrada/capitulo-6-parametros-de-entrada.md>) | inicial | teoria | [PDF](<unidad-06-parametros-de-entrada/fuentes/Capitulo 6-Parametros de Entrada.pdf>) | CON-EPA-U05-PROG-ESTRUCTURADA |
| 7 | Parámetros de entrada/salida | [unidad-07-parametros-de-entrada-salida/capitulo-7-parametros-de-entrada-salida.md](<unidad-07-parametros-de-entrada-salida/capitulo-7-parametros-de-entrada-salida.md>) | inicial | teoria | [PDF](<unidad-07-parametros-de-entrada-salida/fuentes/Capitulo 7-Parametros de Entrada-Salida.pdf>) | CON-EPA-U06-PARAMETROS-ENTRADA |
| 8 | Práctica adicional y exámenes | [unidad-08-practica-adicional/ejercicios-adicionales.md](<unidad-08-practica-adicional/ejercicios-adicionales.md>) | intermedio | ejercicio | [PDF](<unidad-08-practica-adicional/fuentes/Ejercicios Adicionales.pdf>) | CON-EPA-U07-PARAMETROS-ENTRADA-SALIDA |
| 8 | Práctica guiada (con código y animaciones) | [unidad-08-practica-adicional/practica-guiada.md](unidad-08-practica-adicional/practica-guiada.md) | intermedio | ejercicio | (sin PDF propio) | CON-EPA-U08-EJERCICIOS-ADICIONALES |

## Por tema y subtema

| Tema | Subtemas | Unidad |
|---|---|---|
| Presentación del curso | índice general, bienvenida | 0 |
| Introducción al curso | cómo estudiar, recursos complementarios, contenidos | 0 |
| Resolución de problemas | etapas, algoritmo, pre/postcondiciones, secuencia, selección, repetición, iteración, indentación | 1 |
| Algoritmos, lógica y R-info | tipos de lenguajes, sintaxis y semántica, ambiente R-info, estructura de un programa, estilo, estructuras de control, proposiciones y tablas de verdad | 2 |
| Datos y variables | control y datos, representación, variables, tipos de datos, modificación de la información | 3 |
| Repaso integrador | repaso de variables, repaso de expresiones lógicas, ejemplos integradores | 4 |
| Programación estructurada | descomposición de problemas, programación modular, reusabilidad y mantenimiento | 5 |
| Parámetros de entrada | comunicación entre módulos, declaración de parámetros, restricciones | 6 |
| Parámetros de entrada/salida | ejemplos, otro uso de parámetros E/S | 7 |
| Práctica adicional | ejercicios de modularización, exámenes 2013 | 8 |

## Por nivel

- **Inicial:** unidades 0 a 7 (todo el cuerpo teórico del curso de ingreso).
- **Intermedio:** unidad 8 (ejercicios adicionales y exámenes voluntarios, que combinan varios temas del curso).

## Por lenguaje

- **Sin lenguaje formal (pseudocódigo):** unidad 0 (carátula e introducción) y unidad 1 (resolución de problemas, previa a la presentación de R-info).
- **R-info:** unidades 2 a 8 y todo el código en `codigo/ejemplos` y `codigo/soluciones` de cada unidad.

## Por tipo

| Tipo | Archivos |
|---|---|
| resumen | [unidad-00-introduccion/00-caratula.md](unidad-00-introduccion/00-caratula.md) |
| teoria | Unidades 0 a 7 |
| ejercicio | [unidad-08-practica-adicional/ejercicios-adicionales.md](<unidad-08-practica-adicional/ejercicios-adicionales.md>), [unidad-08-practica-adicional/practica-guiada.md](unidad-08-practica-adicional/practica-guiada.md) |

## Ejercicios, soluciones y código relacionado

| Unidad | Enunciados (dentro del capítulo) | Soluciones / código |
|---:|---|---|
| 1 | Sección "Ejercitación" de [unidad-01](<unidad-01-resolucion-de-problemas/capitulo-1-resolucion-de-problemas.md>) | Sin código asociado (ejercicios conceptuales, sin solución en R-info) |
| 2 | Sección "Ejercitación" de [unidad-02](<unidad-02-algoritmos-y-logica/capitulo-2-algoritmos-y-logica.md>) | [codigo/](unidad-02-algoritmos-y-logica/codigo/) (vinculación parcial por nombre; ver nota de procedencia) |
| 3 | Sección "Ejercitación" de [unidad-03](<unidad-03-datos/capitulo-3-datos.md>) | [codigo/](unidad-03-datos/codigo/) |
| 4 | Sección "Ejercitación" de [unidad-04](<unidad-04-repaso/capitulo-4-repaso.md>) | [codigo/soluciones/capitulo-04](unidad-04-repaso/codigo/soluciones/capitulo-04/) |
| 5 | Sección "Ejercitación" de [unidad-05](<unidad-05-programacion-estructurada/capitulo-5-programacion-estructurada.md>) | [codigo/ejemplos/modularizacion](unidad-05-programacion-estructurada/codigo/ejemplos/modularizacion/), [codigo/soluciones/capitulo-05](unidad-05-programacion-estructurada/codigo/soluciones/capitulo-05/) |
| 6 | Sección "Ejercitación" de [unidad-06](<unidad-06-parametros-de-entrada/capitulo-6-parametros-de-entrada.md>) | [codigo/ejemplos/parametros-entrada](unidad-06-parametros-de-entrada/codigo/ejemplos/parametros-entrada/), [codigo/soluciones/capitulo-06](unidad-06-parametros-de-entrada/codigo/soluciones/capitulo-06/) |
| 7 | Sección "Ejercitación" de [unidad-07](<unidad-07-parametros-de-entrada-salida/capitulo-7-parametros-de-entrada-salida.md>) | [codigo/ejemplos/parametros-entrada-salida](unidad-07-parametros-de-entrada-salida/codigo/ejemplos/parametros-entrada-salida/), [codigo/soluciones/capitulo-07](unidad-07-parametros-de-entrada-salida/codigo/soluciones/capitulo-07/) |
| 8 | [ejercicios-adicionales.md](<unidad-08-practica-adicional/ejercicios-adicionales.md>) | [unidad-08-practica-adicional/codigo](unidad-08-practica-adicional/codigo/) (ejercicios 1 a 3 resueltos y detallados en [practica-guiada.md](unidad-08-practica-adicional/practica-guiada.md); 4 a 8 sin solución en el repositorio) |
| — (histórico) | — | [unidad-06-parametros-de-entrada/codigo/archivo-historico/duplicado-capitulo-06](unidad-06-parametros-de-entrada/codigo/archivo-historico/duplicado-capitulo-06/): copia antigua del capítulo 6, conservada por trazabilidad |
| — (entregas) | [Recursos/examen-voluntario.png](../Recursos/examen-voluntario.png) | [Estudiantes/grego](../Estudiantes/grego/), [Estudiantes/valen](../Estudiantes/valen/) |

## Recursos visuales por unidad

| Unidad | Imágenes |
|---:|---|
| 1 | `recursos/figura-1-1-secuencia-original.png` … `figura-1-5-iteracion-original.png` (estructuras de control) |
| 5 | `recursos/figura-5-1-top-down-original.png` … `figura-5-11-recorrido-escalera.png` (Top-Down, recorridos) |
| 6 | `recursos/figura-6-3-top-down-original.png` … `figura-6-7-recorridos-escalones.png` |
| 7 | `recursos/figura-7-1-top-down-original.png` |
| 8 | `recursos/adicional-ejercicio-3-recorrido.png`, `recursos/adicional-ejercicio-5-recorrido.png`, `recursos/ejercicio-01.gif`, `recursos/enunciado.png`, `recursos/sabado.gif` |

Rutas relativas dentro de `recursos/` de cada `unidad-NN-*/` (no hay una carpeta `recursos/` compartida a nivel de `conocimiento/`; las imágenes generales del repositorio están en [../Recursos/](../Recursos/)).

## Notas de procedencia

- Todo el contenido de esta carpeta tiene `origen: "convertido"`: proviene de los 10 PDF, ahora ubicados en `fuentes/` dentro de cada unidad, sin contenido generado por IA durante esta organización (excepto la agrupación editorial de `practica-guiada.md`, que reordena contenido preexistente sin agregar texto nuevo).
- Las unidades 0 y 1 no usan el lenguaje R-info todavía (se presenta recién en la unidad 2), por eso no declaran `lenguajes` en su front matter.
- La vinculación de soluciones históricas de la unidad 2 es parcial a propósito: 10 archivos con nombres ambiguos en el origen no se relacionaron con un ejercicio específico por falta de evidencia suficiente, para no inventar una correspondencia. Se renombraron a `codigo-01.ri`…`codigo-10.ri` (manteniendo su contenido intacto) y quedan disponibles para revisión manual en [unidad-02-algoritmos-y-logica/codigo](unidad-02-algoritmos-y-logica/codigo/). Los nombres originales eran, en ese orden: `1111111111111`, `KK`, `LACONCHADEMIMADRE`, `MANDAR YAAAAAA`, `programa 2`, `programa que anda.enc`, `ROBI`, `ROBOT1`, `siSISISISISISISISI`, `ULTIMO`.
