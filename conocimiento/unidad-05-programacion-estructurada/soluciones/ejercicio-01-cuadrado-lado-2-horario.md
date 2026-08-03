---
id: "EPA-U05-EJ01-SOLUCION"
titulo: "Solución: proceso cuadrado de lado 2 en sentido horario"
slug: "ejercicio-01-cuadrado-lado-2-horario"
tipo: "solucion"
unidad: 5
tema: "programacion-estructurada"
subtemas:
  - "programacion-modular"
  - "procesos-sin-parametros"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 5-Programacion Estructurada.pdf"
    paginas: "1-24"
relacionados:
  - "../ejercicios/ejercicio-01-cuadrado-lado-2-horario.md"
  - "../soluciones/ejercicio-02-recorridos-con-cuadrado.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-05/Cap5_1"
---

# Solución: proceso cuadrado de lado 2 en sentido horario

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-01-cuadrado-lado-2-horario.md`](../ejercicios/ejercicio-01-cuadrado-lado-2-horario.md).

## Análisis

Un cuadrado de lado 2 tiene 4 lados iguales, cada uno de 2 esquinas de longitud. Recorrer un lado implica avanzar (`mover`) 2 veces con la orientación actual del robot; al llegar a un vértice, girar 90° en sentido horario (`derecha`) deja al robot orientado para recorrer el lado siguiente. Repitiendo esta secuencia (2 avances + 1 giro) cuatro veces, el robot recorre los cuatro lados y vuelve a quedar parado en la esquina de partida, con la misma orientación que tenía al invocar el proceso — esta es exactamente la propiedad que describe el Ejemplo 5.6 de la teoría del capítulo para su propio módulo `cuadrado` de lado 2.

Este es el patrón de descomposición Top-Down más simple del capítulo: un único proceso, sin sub-procesos ni parámetros, que encapsula una figura reutilizable.

## Estrategia

1. Definir el proceso `cuadrado`.
2. Repetir 4 veces: avanzar 2 esquinas (`repetir 2: mover`) y girar a la derecha.
3. Invocar `cuadrado` una vez desde el cuerpo del robot.

## Código relacionado

```
programa prueba
procesos
  proceso izquierda
  comenzar
    repetir 3
      derecha
  fin
  proceso cuadrado
  comenzar
    repetir 4
      repetir 2
        mover
      derecha
  fin
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  variables
    vacias: numero
  comenzar
    vacias:=0
    cuadrado
  fin
variables
  robin:robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-05/Cap5_1`](<../codigo/soluciones/capitulo-05/Cap5_1>)

## Corrección aplicada durante esta organización

El archivo histórico tenía `repetir 3` en el cuerpo interno de `cuadrado` (es decir, un cuadrado de **lado 3**), en contradicción con tres fuentes independientes que coinciden en que el lado debía ser 2: el propio enunciado ("cuadrado de lado 2"), el comentario `{...}` del archivo (que repite el enunciado literalmente) y el módulo `cuadrado` de lado 2 que la teoría de este mismo capítulo define explícitamente en el Ejemplo 5.6 (`repetir 4: repetir 2: mover; derecha`). Se corrigió el `repetir 3` interno a `repetir 2` sin tocar el resto de la estructura (la cantidad de lados, el sentido de giro y el proceso `izquierda` —no usado en este ejercicio— quedaron igual).

Nota de alcance: el proceso `cuadrado` con este mismo `repetir 3` (sin usar, como código heredado del mismo bloque de `procesos`) también aparecía copiado en los archivos de los ejercicios 3 y 4 de este capítulo, donde nunca se invoca. Se corrigió por consistencia en esas copias también (ver sus soluciones), aunque no cambia el comportamiento de esos programas al ser código muerto.

Las variables `vacias: numero` y la asignación `vacias:=0` en el archivo histórico tampoco se usan en ningún lugar del programa; es otro resabio de copiar la plantilla de un ejercicio distinto. No se quitaron por no ser un error de comportamiento (declarar una variable no utilizada no afecta el recorrido del robot).

## Escenario de prueba

Alcanza con correr el programa sobre una ciudad vacía (sin flores ni papeles) — el proceso `cuadrado` no depende del contenido de las esquinas, solo del movimiento y el giro. Para verificarlo visualmente conviene observar la posición final del robot: debe volver a (1,1), la misma esquina de partida, orientado igual que al inicio.

## Casos límite

- Si se invoca `cuadrado` cerca del borde superior del área (`AreaC(1,1,100,100)`, por ejemplo con el robot en avenida o calle 99 o 100), el recorrido de lado 2 puede salirse del área válida y el intérprete corta la ejecución con un error de "se salió de la ciudad".
- El proceso no altera el contenido de las esquinas (no junta ni deja flores/papeles): solo mueve al robot y lo gira.

## Errores frecuentes

- Confundir "lado 2" con "2 giros" o con "repetir 2" en el bucle exterior (que en realidad debe ser `repetir 4`, uno por cada lado del cuadrado); el 2 corresponde a la cantidad de `mover` por lado, no a la cantidad de lados.
- Girar en sentido antihorario (usar el proceso `izquierda` en vez de `derecha` directamente) cuando el enunciado pide explícitamente sentido horario.

## Complejidad

Un recorrido fijo de 8 movimientos y 4 giros por invocación: O(1) respecto al tamaño de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-01-cuadrado-lado-2-horario.md`](../ejercicios/ejercicio-01-cuadrado-lado-2-horario.md)
- Fuente original: [`../fuentes/Capitulo 5-Programacion Estructurada.pdf`](<../fuentes/Capitulo 5-Programacion Estructurada.pdf>)
- Código: [`../codigo/soluciones/capitulo-05/Cap5_1`](<../codigo/soluciones/capitulo-05/Cap5_1>)
- Teoría de referencia: Ejemplo 5.6 en [`../capitulo-5-programacion-estructurada.md`](<../capitulo-5-programacion-estructurada.md>), que define el mismo módulo `cuadrado` de lado 2.
