---
id: "EPA-U03-EJ05-SOLUCION"
titulo: "Solución: caminar la calle 7 hasta encontrar 20 flores (pueden no existir)"
slug: "ejercicio-05-veinte-flores-calle-7-pueden-no-existir"
tipo: "solucion"
unidad: 3
tema: "datos-y-variables"
subtemas:
  - "variables"
  - "estructuras-de-control"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 3-Datos.pdf"
    paginas: "1-21"
relacionados:
  - "../ejercicios/ejercicio-05-veinte-flores-calle-7-pueden-no-existir.md"
  - "../soluciones/ejercicio-04-veinte-flores-calle-7-garantizadas.md"
codigo_relacionado:
  - "../codigo/capitulo-3-pregunta-05.ri"
escenario_ciudad:
  - av: 5
    ca: 7
    flores: 1
  - av: 10
    ca: 7
    flores: 1
  - av: 15
    ca: 7
    flores: 1
  - av: 20
    ca: 7
    flores: 1
  - av: 25
    ca: 7
    flores: 1
  - av: 30
    ca: 7
    flores: 1
  - av: 35
    ca: 7
    flores: 1
  - av: 40
    ca: 7
    flores: 1
---

# Solución: caminar la calle 7 hasta encontrar 20 flores (pueden no existir)

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-05-veinte-flores-calle-7-pueden-no-existir.md`](../ejercicios/ejercicio-05-veinte-flores-calle-7-pueden-no-existir.md).

## Análisis

A diferencia del ejercicio 4, acá no se garantiza que existan 20 flores, así que el corte del recorrido no puede depender sólo de `x<20`: hace falta combinarlo con el límite de la calle (`PosAv<100`). El robot avanza mientras no se acabó la calle; en cada esquina, sólo si todavía no llegó a 20 flores intenta tomar una.

## Estrategia

1. Posicionar el robot en (1,7) y girar a la derecha.
2. Mientras `PosAv<100`: si `x<20` y hay flor en la esquina, tomarla y contarla; avanzar (siempre, haya o no encontrado flor).
3. Procesar la esquina final (avenida 100) con el mismo chequeo, sin avanzar más, ya que el `mientras` deja de ejecutarse justo antes de revisarla.
4. Informar `x`.

## Código relacionado

```rinfo
programa prueba
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  variables
    x: numero
    y: numero
  comenzar
    Pos(1,7)
    x:=0
    derecha
    mientras(PosAv<100)
      si(x<20)
        si(HayFlorEnLaEsquina)
          tomarFlor
          x:=x+1
      mover
    si(x<20)
      si(HayFlorEnLaEsquina)
        tomarFlor
        x:=x+1
    Informar(x)
  fin
variables
  robin:robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/capitulo-3-pregunta-05.ri`](../codigo/capitulo-3-pregunta-05.ri)

## Correcciones aplicadas durante esta organización

Se aplicaron dos correcciones, ambas verificadas con el intérprete de R-info:

1. **`mover` mal anidado (loop infinito):** en el archivo histórico, `mover` estaba anidado **dentro** del `si(x<20)`, en vez de ser una instrucción del cuerpo del `mientras(PosAv<100)` que se ejecuta siempre. El efecto: en cuanto `x` llegaba a 20 antes de que `PosAv` llegara a 100, `mover` dejaba de ejecutarse (porque `x<20` ya era falso), con lo cual `PosAv` quedaba congelado y el `mientras(PosAv<100)` exterior nunca terminaba — un loop infinito. Se verificó con el intérprete: cargando 20 flores en las avenidas 1 a 20 de la calle 7, el archivo original se cuelga (supera el límite de pasos del intérprete, señal de loop infinito); con `mover` desanidado (al mismo nivel que `si(x<20)`) el programa informa correctamente `x=20` y termina.
2. **Avenida 100 sin chequear (bug de alcance, corregido en esta pasada):** aun con `mover` desanidado, el `mientras(PosAv<100)` dejaba de procesar esquinas apenas `PosAv` llegaba a 100 — la esquina (100,7) nunca se chequeaba, así que si la flor número 20 estuviera justo ahí, el programa informaba un valor menor a 20 pese a que sí había 20 flores en la calle. Se corrigió agregando, después del `mientras`, el mismo chequeo `si(x<20) si(HayFlorEnLaEsquina) tomarFlor x:=x+1` que ya usa el cuerpo del bucle, para procesar esa última esquina sin volver a mover. Verificado con el intérprete: con 19 flores en las avenidas 1-19 y la flor número 20 puesta exactamente en la avenida 100, el archivo (sólo con el fix de `mover`) informaba `x=19`; con esta segunda corrección informa `x=20`. También se re-probó sin flores (informa `x=0`, sin colgarse) y con las 20 flores en avenidas 1-20 (informa `x=20`, sin overshoot ni error), confirmando que ninguna de las dos correcciones introdujo una regresión.

## Escenario de prueba

Cargá menos de 20 flores en la calle 7, salteadas. Con 8 flores, en las avenidas 5, 10, 15, 20, 25, 30, 35 y 40, el robot recorre la calle entera, informa `8` y termina en la avenida 100.

## Casos límite

- Calle sin ninguna flor: informa `0` y termina igual.
- Si la flor número 20 está justo en la avenida 100, se cuenta: de eso se ocupa el `si(x<20)` suelto que va después del `mientras`. Informa `20`.
- Cuando `x` llega a 20 el robot deja de recoger, pero sigue caminando hasta el final de la calle. El enunciado no le pide frenar ahí.

## Errores frecuentes

- Meter el `mover` adentro del `si(x<20)`. Apenas juntás las 20 flores el robot deja de avanzar, `PosAv` se congela y el `mientras(PosAv<100)` no termina nunca. En R-info no hay `break`: si la instrucción que empuja la condición de corte queda tapada por un `si`, el bucle se cuelga.
- Quedarse sólo con el `mientras(PosAv<100)`. Ese bucle frena cuando `PosAv` vale 100, así que nunca llega a mirar esa esquina. Por eso va el chequeo suelto de después.

## Complejidad

Recorrido de hasta 100 esquinas (una calle completa): O(1) respecto al tamaño de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-05-veinte-flores-calle-7-pueden-no-existir.md`](../ejercicios/ejercicio-05-veinte-flores-calle-7-pueden-no-existir.md)
- Código: [`../codigo/capitulo-3-pregunta-05.ri`](../codigo/capitulo-3-pregunta-05.ri)
