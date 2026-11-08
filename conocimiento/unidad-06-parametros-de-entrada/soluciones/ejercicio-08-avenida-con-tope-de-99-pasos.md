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

```rinfo
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

Ciudad vacía, sin flores ni papeles. El programa invoca `Avenida(4,200)`: el tope baja los 200 a 99, así que el robot sale de (4,1) y sube hasta (4,100), justo el borde de la ciudad.

## Casos límite

- Con un `pasos` negativo, `pasosReales` queda negativo y no entra en el `si`. Un `repetir` con un número negativo no ejecuta el cuerpo: el robot se reposiciona en la avenida pedida y no avanza, que es lo que pide el enunciado.
- El `si` recorta recién a partir de 100. Un `pasos` de 99 pasa tal cual y da los 99 pasos.

## Errores frecuentes

- Escribir `pasos:=99` adentro del proceso. `pasos` es un parámetro de entrada: solo se puede leer. Por eso el tope se calcula sobre `pasosReales`, una variable local.
- Agregar un `si (pasosReales<0) pasosReales:=0`. No hace falta: `repetir` con un negativo ya no da ningún paso.

## Complejidad

El recorrido tiene como máximo 99 pasos, sin importar el valor recibido: O(1) respecto del parámetro `pasos` (acotado por la restricción del propio enunciado).

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-08-avenida-con-tope-de-99-pasos.md`](../ejercicios/ejercicio-08-avenida-con-tope-de-99-pasos.md)
- Código: [`../codigo/soluciones/capitulo-06/Cap6_Preg_8`](../codigo/soluciones/capitulo-06/Cap6_Preg_8)
