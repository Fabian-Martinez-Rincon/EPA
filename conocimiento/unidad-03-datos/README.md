# Unidad 3 — Datos y variables

Conceptos de control y datos, representación de la información, declaración de variables y los tipos de datos numérico y lógico (boolean).

- [capitulo-3-datos.md](<capitulo-3-datos.md>) — teoría completa + ejercitación (ejercicios 1 a 10).
- Fuente: [fuentes/](fuentes/).
- Código: [codigo/](codigo/) — un archivo `.ri` por ejercicio, nombrados `capitulo-3-pregunta-02.ri` a `capitulo-3-pregunta-10.ri` (el ejercicio 1 no tiene archivo propio, ver más abajo).

## Ejercicios atomizados (`ejercicios/` + `soluciones/`)

Igual que en `AYP1-FABOSISTEMAS` y en `unidad-02-algoritmos-y-logica`, 8 de los 10 ejercicios de este capítulo están atomizados uno por archivo, con front matter YAML y solución explicada (análisis, estrategia, casos límite, errores frecuentes) en [ejercicios/](ejercicios/) y [soluciones/](soluciones/): ejercicios **2, 3, 4, 5, 6, 8, 9 y 10**.

Durante esta atomización, y en una auditoría posterior de ejecución real contra el intérprete, se encontraron y corrigieron 5 bugs puntuales en total (tres de ellos loops infinitos confirmados con el intérprete de R-info de Academia-Fabo, dos más de alcance incompleto):

- `codigo/capitulo-3-pregunta-03.ri`: faltaba el operador `|` entre dos proposiciones atómicas en una condición negada, lo que directamente impedía parsear el archivo. Se agregó, igualando las otras dos apariciones de la misma condición en el archivo. Además, aun con el `|` corregido, el archivo dejaba sin revisar 99 de las 100 esquinas de la calle 100 (el `repetir 99` exterior nunca recorría esa última calle por completo, sólo chequeaba una esquina suelta) — confirmado informando 9901 en vez de 10000 sobre una ciudad vacía. Se corrigió agregando, después del `repetir` exterior, el mismo bloque `repetir 99 {chequeo; mover}` + chequeo final que ya usa cada calle dentro del bucle; con la corrección, la ciudad vacía informa 10000.
- `codigo/capitulo-3-pregunta-05.ri`: la instrucción `mover` estaba mal anidada dentro de una condición (`si(x<20)`) que podía volverse falsa antes de que el bucle exterior (`mientras(PosAv<100)`) terminara, causando un loop infinito apenas se juntaban las 20 flores antes de llegar al final de la calle. Confirmado con el intérprete (el archivo original se cuelga con 20 flores cargadas); se corrigió desanidando `mover`. Además, el `mientras(PosAv<100)` nunca procesaba la esquina de la avenida 100, así que una flor ubicada ahí no se contaba — se corrigió agregando, después del `mientras`, el mismo chequeo de flor que usa el cuerpo del bucle, para procesar esa última esquina.
- `codigo/capitulo-3-pregunta-08.ri`: el mismo tipo de bug que en `pregunta-05` (mismo `mover` mal anidado, mismo loop infinito confirmado con el intérprete), más un límite de recorrido incompleto (`PosAv<99` en vez de `PosAv<100`, que dejaba la avenida 100 sin revisar). Se corrigieron ambos.

Cada corrección está documentada en detalle en la solución correspondiente, bajo "Correcciones aplicadas durante esta organización", incluyendo los escenarios de prueba usados para confirmarla con el intérprete. Los 8 ejercicios atomizados de esta unidad están en estado `"completo"`.

## Ejercicios pendientes (sin atomizar)

- **Ejercicio 1**: es un ejercicio de tipo "indique qué hace este programa" (con sub-casos a evaluar), no de "escriba un programa"; su código ya está embebido y resuelto dentro de `capitulo-3-datos.md` y no tiene un archivo `.ri` propio ni aparece en la tabla "Código relacionado con la ejercitación" del capítulo. No se atomiza junto con los ejercicios de "escriba un programa", siguiendo el mismo criterio que con los ejercicios sin código de unidad-02.
- **Ejercicio 7** (`codigo/capitulo-3-pregunta-07.ri`): el enunciado pide contar cuántas esquinas de la calle 34 tenían originalmente **exactamente** 6 papeles, pero el código tiene varios problemas entrelazados, no un fix quirúrgico: la variable `y` que cuenta papeles de la esquina actual nunca se reinicia a 0 entre esquinas (se acumula a lo largo de todo el recorrido), y la condición `si(y>=6)` se evalúa en cada papel tomado (no una sola vez por esquina) y usa `>=` en lugar de `=`. Se verificó con el intérprete de R-info: con dos esquinas que tienen exactamente 6 papeles cada una (la respuesta correcta es 2), el código informa **7**. Corregir esto exigiría reiniciar `y` dentro del `repetir`, mover el chequeo fuera del `mientras` de toma de papeles y cambiar el operador — un conjunto de cambios que reescribe la lógica de conteo, no un ajuste puntual. Queda pendiente.

**Prerrequisitos:** [unidad-02-algoritmos-y-logica](../unidad-02-algoritmos-y-logica/).

**Siguiente unidad:** [unidad-04-repaso](../unidad-04-repaso/).
