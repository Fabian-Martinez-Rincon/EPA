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

```rinfo
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

Corré el programa sobre una ciudad vacía. `cuadrado` no mira flores ni papeles: sólo mueve y gira.

Fijate dónde termina el robot. Sale de (1,1), recorre el borde del bloque que llega hasta (3,3) y vuelve a (1,1) mirando para el mismo lado que al arrancar.

## Casos límite

- `cuadrado` necesita 2 esquinas de lugar en avenida y en calle. Desde la avenida 98 entra; desde la 99 el robot se sale de la ciudad y el programa corta.
- El robot vuelve a la esquina de partida con la misma orientación. Por eso podés invocarlo una y otra vez sin llevar la cuenta de los giros.

## Errores frecuentes

- Dar vuelta los dos `repetir`. El `repetir 4` son los cuatro lados; el `repetir 2` de adentro, los dos `mover` de cada lado. Al revés el robot dibuja una L de dos tramos de 4 y queda en (5,5).
- Usar `izquierda` en vez de `derecha`. El enunciado pide sentido horario. Y desde (1,1) el robot sube a (1,3), dobla hacia las avenidas decrecientes y se sale de la ciudad.

## Complejidad

Un recorrido fijo de 8 movimientos y 4 giros por invocación: O(1) respecto al tamaño de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-01-cuadrado-lado-2-horario.md`](../ejercicios/ejercicio-01-cuadrado-lado-2-horario.md)
- Código: [`../codigo/soluciones/capitulo-05/Cap5_1`](<../codigo/soluciones/capitulo-05/Cap5_1>)
- Teoría de referencia: Ejemplo 5.6 en [`../capitulo-5-programacion-estructurada.md`](<../capitulo-5-programacion-estructurada.md>), que define el mismo módulo `cuadrado` de lado 2.
