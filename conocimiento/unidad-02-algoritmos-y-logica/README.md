# Unidad 2 — Algoritmos, lógica y el lenguaje R-info

Introducción al ambiente de programación del robot R-info: sintaxis, estructura de un programa, las estructuras de control ya vistas pero escritas en R-info, y una introducción a proposiciones lógicas y tablas de verdad.

- [capitulo-2-algoritmos-y-logica.md](<capitulo-2-algoritmos-y-logica.md>) — teoría completa + ejercitación (12 ejercicios).
- Fuente: [fuentes/](fuentes/).
- Código: [codigo/](codigo/) — un archivo `.ri` por solución; los que no se pudieron asociar a un ejercicio puntual sin evidencia suficiente quedaron como `codigo-01.ri`…`codigo-10.ri` (ver la nota de procedencia en el [índice general](../INDICE_GENERAL.md)).

## Ejercicios atomizados (`ejercicios/` + `soluciones/`)

Igual que en `AYP1-FABOSISTEMAS`, 7 de los 12 ejercicios de este capítulo ya están atomizados uno por archivo, con front matter YAML y solución explicada (análisis, estrategia, casos límite, errores frecuentes) en [ejercicios/](ejercicios/) y [soluciones/](soluciones/): ejercicios **2, 4, 6, 7, 9, 11 y 12**. Es la base que usa [Academia-Fabo](https://github.com/Fabian-Martinez-Rincon/Academia-Fabo) para mostrarlos con un runner de R-info en el navegador.

Durante esta atomización se revisó el código `.ri` de cada uno contra su propio enunciado (mismo estándar que en AYP1) y se encontraron y corrigieron varios bugs heredados del material histórico — código que usaba flor donde el enunciado pedía papel, una condición de "esquina libre" invertida, y (en una revisión posterior) un recorrido que se salía del área y solo cubría una calle:

- `codigo/ejercicio-02.ri`: usaba `HayFlorEnLaBolsa`/`depositarFlor`, corregido a `HayPapelEnLaBolsa`/`depositarPapel`.
- `codigo/ejercicio-09.ri`: mismo tipo de corrección (flor → papel).
- `codigo/ejercicio-12.ri`: la condición de "esquina libre" estaba invertida (depositaba donde YA había flor y papel), se salía del área válida por un `repetir 100` donde correspondía `repetir 99`, y solo recorría la calle 1 en vez de las 100 que pide el enunciado. Los tres problemas se corrigieron: condición negada, límite del `repetir` ajustado, y todo el recorrido de una calle envuelto en un `repetir 100` adicional (una vuelta por calle). Ver el detalle en su solución.

Cada corrección está documentada en detalle en la solución correspondiente, bajo "Corrección aplicada durante esta organización".

## Ejercicios pendientes (sin atomizar)

- **Ejercicios 1, 3 y 5**: no tienen código identificado con evidencia suficiente (mismo criterio que `codigo-01.ri`…`codigo-10.ri`); no se atomizan para no inventar contenido.
- **Ejercicio 8** (`codigo/ejercicio-08.ri`): el código no solo confunde flor/papel, también gira hacia el eje equivocado (recorre la calle 1 en vez de la avenida 23) y nunca llega a depositar ni informar — son varios problemas entrelazados, no un fix quirúrgico. Queda pendiente de una reescritura futura.
- **Ejercicio 10** (`codigo/ejercicio-10.ri`): el código recorre el perímetro completo de la ciudad juntando solo papeles, no "las 5 primeras avenidas" juntando flores y papeles como pide el enunciado — resuelve un problema distinto. Queda pendiente.
- **`codigo/ejercicio-07-1.ri`, `ejercicio-07-4.ri`, `ejercicio-07-5.ri`**: comparten el comentario de enunciado del ejercicio 7, pero implementan un problema distinto (contar flores/papeles por avenida e informar totales). Quedan sin atomizar junto con `codigo-01.ri`…`codigo-10.ri`, pendientes de identificar a qué ejercicio corresponden realmente.

**Prerrequisitos:** [unidad-01-resolucion-de-problemas](../unidad-01-resolucion-de-problemas/).

**Siguiente unidad:** [unidad-03-datos](../unidad-03-datos/).
