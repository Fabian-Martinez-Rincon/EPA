---
id: "EPA-U06-EJ08-SOLUCION"
titulo: "Solución: recorrer una avenida una cantidad de pasos, con tope de 99"
slug: "ejercicio-08-avenida-con-tope-de-99-pasos"
tipo: "solucion"
unidad: 6
tema: "parametros-de-entrada"
subtemas:
  - "declaracion-de-parametros"
  - "restriccion-en-el-uso-de-parametros-de-entrada"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 6-Parametros de Entrada.pdf"
    paginas: "1-20"
relacionados:
  - "../ejercicios/ejercicio-08-avenida-con-tope-de-99-pasos.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_8"
---

# Solución: recorrer una avenida una cantidad de pasos, con tope de 99

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-08-avenida-con-tope-de-99-pasos.md`](../ejercicios/ejercicio-08-avenida-con-tope-de-99-pasos.md).

## Análisis

El proceso `Avenida(E Numero:numero; E pasos:numero)` se reposiciona en `(Numero,1)` (sin girar: la orientación por defecto ya avanza a lo largo de la avenida) y avanza tantas veces como indique `pasos`, acotado a 99. El caso "valor negativo no debe dar pasos" no necesita una comparación explícita: en R-info, `repetir N` con `N` negativo o cero simplemente no ejecuta el cuerpo ninguna vez (el intérprete lo trata como un bucle `for` estándar que nunca entra si el contador ya supera el límite), así que un `pasos` negativo pasa derecho por el único `si` de acotación superior y termina en un `repetir` que no mueve al robot.

## Estrategia

1. Declarar `proceso Avenida(E Numero:numero; E pasos:numero)`.
2. Reposicionar con `Pos(Numero,1)`.
3. Copiar el parámetro `pasos` en una variable local (`pasosReales`) y, si supera 99, acotarla a 99.
4. Avanzar `pasosReales` veces (0 veces si el valor original era negativo).

## Código relacionado

```
programa  parametros
procesos
  proceso izquierda
  comenzar
    repetir 2
      derecha
  fin
  proceso Avenida(E Numero:numero;E pasos:numero)
  variables
    noventa:numero
    pasosReales:numero
  comenzar
    Pos(Numero,1)
    noventa:=99
    pasosReales:=pasos
    si (pasosReales>99)
      pasosReales:=noventa
    repetir pasosReales
      mover
  fin
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  variables
    NAvenida:numero
    CantPasos:numero
  comenzar
    CantPasos:=200
    NAvenida:=4
    Avenida(NAvenida,CantPasos)
  fin
variables
  robin: robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-06/Cap6_Preg_8`](../codigo/soluciones/capitulo-06/Cap6_Preg_8)

## Corrección aplicada durante esta organización

El archivo histórico hacía `pasos:=noventa` **dentro** del proceso, asignando un valor a `pasos`, que está declarado como parámetro de entrada (`E`). Esto viola exactamente la restricción que el propio capítulo explica en la sección 6.5 ("Restricción en el uso de los parámetros de entrada"): un parámetro de entrada solo se puede leer, nunca modificar dentro del proceso que lo recibe; el capítulo incluso muestra este mismo error en el Ejemplo 6.6 (`UnaMenosV1`, que asigna sobre un parámetro `E`) y lo corrige introduciendo una variable local auxiliar (`UnaMenosV2`). Se aplicó exactamente esa misma corrección aquí: se agregó la variable local `pasosReales`, se copió `pasos` en ella al entrar al proceso, y el resto de la lógica (la comparación con 99 y el `repetir`) pasó a operar sobre `pasosReales` en vez de sobre el parámetro de entrada. El comportamiento observable no cambia — el intérprete de Academia-Fabo no impedía la asignación original y el resultado numérico era el mismo — pero el código ya no comete la infracción sintáctica que este mismo capítulo dedica una sección a explicar.

## Escenario de prueba

No requiere flores ni papeles precargados: alcanza con observar que, con `NAvenida:=4` y `CantPasos:=200`, el robot avanza exactamente 99 cuadras en la avenida 4 (200 se acota a 99).

## Casos límite

- `pasos` negativo (por ejemplo, -5): `pasosReales` queda en -5, no es mayor que 99, y `repetir -5 mover` no ejecuta ningún paso — el robot se reposiciona en la avenida pedida pero no avanza, tal como exige el enunciado.
- `pasos` mayor que 99 (como en el ejemplo del archivo, 200): se acota a 99.
- `pasos` entre 0 y 99 (por ejemplo, 5): se usa tal cual, sin acotar.
- El proceso auxiliar `izquierda` queda declarado pero no se usa en este archivo; no afecta el resultado.

## Errores frecuentes

- Asignar directamente sobre el parámetro de entrada en vez de usar una variable local auxiliar (el bug real que tenía este archivo antes de esta organización).
- Agregar una comparación explícita para el caso negativo (`si (pasosReales<0) pasosReales:=0`): es innecesaria, porque `repetir` con un valor negativo ya no ejecuta el cuerpo ninguna vez; agregarla no sería incorrecto, pero tampoco es lo que hace el material original.

## Complejidad

El recorrido tiene como máximo 99 pasos, sin importar el valor recibido: O(1) respecto del parámetro `pasos` (acotado por la restricción del propio enunciado).

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-08-avenida-con-tope-de-99-pasos.md`](../ejercicios/ejercicio-08-avenida-con-tope-de-99-pasos.md)
- Fuente original: [`../fuentes/Capitulo 6-Parametros de Entrada.pdf`](<../fuentes/Capitulo 6-Parametros de Entrada.pdf>)
- Código: [`../codigo/soluciones/capitulo-06/Cap6_Preg_8`](../codigo/soluciones/capitulo-06/Cap6_Preg_8)
