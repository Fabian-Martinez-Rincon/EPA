# Unidad 7 — Parámetros de entrada/salida

Procesos que reciben y devuelven información modificada mediante parámetros de entrada/salida (`ES`).

- [capitulo-7-parametros-de-entrada-salida.md](<capitulo-7-parametros-de-entrada-salida.md>) — teoría completa + ejercitación (6 ejercicios).
- Fuente: [fuentes/](fuentes/).
- Figuras: [recursos/](recursos/).
- Código:
  - [codigo/ejemplos/parametros-entrada-salida](codigo/ejemplos/parametros-entrada-salida/) — ejemplos de apoyo (Ejemplos 7.1-7.5 del capítulo, más dos demos sueltas), ya identificados en el comentario de cada archivo; no son ejercicios numerados y no se atomizan.
  - [codigo/soluciones/capitulo-07](codigo/soluciones/capitulo-07/) — `Cap7_Preg_1` a `Cap7_Preg_6` (+ variante `CAP7PREG3`) corresponden a los 6 ejercicios de la Ejercitación del capítulo; `Cap7_Preg_7` a `Cap7_Preg_14` no tienen enunciado original identificado (ver comentario de cada archivo) y quedan fuera de esta atomización.

## Ejercicios atomizados (`ejercicios/` + `soluciones/`)

De los 6 ejercicios de la Ejercitación, **2 quedaron atomizados** uno por archivo, con front matter YAML y solución explicada en [ejercicios/](ejercicios/) y [soluciones/](soluciones/): ejercicios **5 y 6**.

- **Ejercicio 6** (`codigo/soluciones/capitulo-07/Cap7_Preg_6`, estado `completo`): se corrigieron dos bugs quirúrgicos, verificados contra el intérprete de R-info de Academia-Fabo — `lado:=14` (valor de prueba sin revertir) corregido a `lado:=99` como pide el enunciado, y la condición de corte `mientras(~(flores=3)&~(papeles=2))` corregida a `mientras(~(flores=3)|~(papeles=2))` (De Morgan aplicado al revés: con `&` el recorrido se detenía apenas se cumplía UNA de las dos condiciones, no ambas). Ver el detalle y la prueba diferencial en su solución.
- **Ejercicio 5** (`codigo/soluciones/capitulo-07/Cap7_Preg_5`, estado `parcial`): la lógica de recorrido y conteo de pasos es correcta y se verificó que las 50 calles impares se informan bien, pero el `repetir 99` del programa principal excede las 50 calles impares reales; al llegar a la calle 99 el proceso `CallesImpares` intenta reposicionarse incondicionalmente a la calle 101 (inexistente) y el intérprete corta la ejecución. No se corrigió por ser un problema de alcance (acotar el `repetir` no alcanza, ver el detalle en la solución), pero se documentó que el corte ocurre recién después de que las 50 esquinas buscadas ya fueron informadas correctamente.

## Ejercicios pendientes (sin atomizar)

- **Ejercicio 1** (`codigo/soluciones/capitulo-07/Cap7_Preg_1`): el enunciado pide explícitamente "utilice un proceso que recorra una calle cuyo número recibe como parámetro"; el código declara ese parámetro (`E calle`) pero lo usa solo para la posición inicial y hace todo el doble recorrido de la ciudad **dentro** del proceso en una única invocación, en vez de que el programa principal invoque el proceso una vez por calle. Probado contra el intérprete, corre sin errores pero subcuenta sistemáticamente (nunca cuenta la esquina de avenida 100 de cada calle, ni recorre la calle 100). No se atomiza por ser un problema de diseño/descomposición, no un fix de una palabra.
- **Ejercicio 2** (`codigo/soluciones/capitulo-07/Cap7_Preg_2`): tiene un bug quirúrgico real (`flores:=0` al inicio de `trasladar` descarta el acumulador `ES` en cada llamada, en vez de dejar que el llamador lo inicialice una sola vez), pero además tiene el mismo problema de reposicionamiento incondicional que el ejercicio 5 — y en este caso el corte ocurre **antes** de llegar al `Informar` final (que está fuera del loop principal, no dentro de cada llamada), así que el programa nunca llega a informar el total pedido por el enunciado, ni siquiera arreglando el bug del acumulador. Verificado con y sin ese fix contra el intérprete: en ambos casos el error `Pos(1,101) está fuera del área` corta la ejecución antes de cualquier `Informar`. No se atomiza porque el resultado que pide el enunciado nunca se produce.
- **Ejercicio 3** (`codigo/soluciones/capitulo-07/Cap7_Preg_3` y su variante `CAP7PREG3`): ambas implementaciones resuelven un problema distinto del enunciado. `Cap7_Preg_3` mezcla el conteo de flores/papeles de la esquina inicial (1,1) con el recorrido de la avenida 9, y deposita indiscriminadamente una flor y un papel en cada esquina de la avenida en vez de calcular "lo que haga falta" por esquina — probado contra el intérprete llega a informar cantidades negativas. La variante `CAP7PREG3` además cuenta flores donde debería contar papeles (`ContarP` usa `HayFlorEnLaEsquina`/`tomarFlor`), tiene un parámetro `E seguir:boolean` que debería ser `ES` (el proceso `DepoP` nunca puede comunicarle al llamador que hay que detener el recorrido), usa literales booleanos `V`/`F` que el intérprete de R-info de Academia-Fabo no reconoce (ver limitación abajo) y además usa `boolean` como nombre de tipo en vez de `logico`, lo que directamente impide que el archivo parsee. Son demasiados problemas entrelazados para un fix quirúrgico.
- **Ejercicio 4** (`codigo/soluciones/capitulo-07/Cap7_Preg_4`): el proceso `calle` hace un `derecha` en cada invocación sin deshacerlo nunca, así que la orientación del robot rota 90° cada vez que se llama (una vez por calle, 99 veces); probado contra el intérprete, el robot se sale de la ciudad al segundo `mover` del programa principal, apenas terminada la primera calle. Además el proceso `SinModificar` no resuelve "depositar una flor o un papel según el total de la calle" como pide el enunciado, sino que balancea flor contra papel esquina por esquina. No se atomiza por tratarse de varios problemas de diseño entrelazados, no un fix puntual.

## Limitaciones del intérprete de R-info detectadas durante esta organización

Ninguna afecta a los ejercicios atomizados (5 y 6), pero quedan documentadas porque aparecen en varios archivos históricos del repositorio, no solo en unidad 7:

- El tipo booleano solo se reconoce como `logico`; la palabra `boolean` (usada en `codigo/ejemplos/parametros-entrada-salida/basico.ri` de esta misma unidad, en `CAP7PREG3`, y en varios archivos de `unidad-02-algoritmos-y-logica/codigo/`) hace que el parser falle con "Se esperaba un tipo (numero/logico)".
- Los literales booleanos solo se reconocen como `verdadero`/`falso`; la abreviatura `V`/`F` (usada en `CAP7PREG3` y en `unidad-02-algoritmos-y-logica/codigo/codigo-07.ri`) se interpreta como una variable no declarada y falla en tiempo de ejecución, no en el parseo.

**Prerrequisitos:** [unidad-06-parametros-de-entrada](../unidad-06-parametros-de-entrada/).

**Siguiente unidad:** [unidad-08-practica-adicional](../unidad-08-practica-adicional/).
