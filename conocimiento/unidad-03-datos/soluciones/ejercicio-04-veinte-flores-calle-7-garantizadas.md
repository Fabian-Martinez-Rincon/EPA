---
id: "EPA-U03-EJ04-SOLUCION"
titulo: "Solución: caminar la calle 7 hasta encontrar 20 flores (garantizadas)"
slug: "ejercicio-04-veinte-flores-calle-7-garantizadas"
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
  - "../ejercicios/ejercicio-04-veinte-flores-calle-7-garantizadas.md"
  - "../soluciones/ejercicio-05-veinte-flores-calle-7-pueden-no-existir.md"
codigo_relacionado:
  - "../codigo/capitulo-3-pregunta-04.ri"
escenario_ciudad:
  - av: 1
    ca: 7
    flores: 1
  - av: 2
    ca: 7
    flores: 1
  - av: 3
    ca: 7
    flores: 1
  - av: 4
    ca: 7
    flores: 1
  - av: 5
    ca: 7
    flores: 1
  - av: 6
    ca: 7
    flores: 1
  - av: 7
    ca: 7
    flores: 1
  - av: 8
    ca: 7
    flores: 1
  - av: 9
    ca: 7
    flores: 1
  - av: 10
    ca: 7
    flores: 1
  - av: 11
    ca: 7
    flores: 1
  - av: 12
    ca: 7
    flores: 1
  - av: 13
    ca: 7
    flores: 1
  - av: 14
    ca: 7
    flores: 1
  - av: 15
    ca: 7
    flores: 1
  - av: 16
    ca: 7
    flores: 1
  - av: 17
    ca: 7
    flores: 1
  - av: 18
    ca: 7
    flores: 1
  - av: 19
    ca: 7
    flores: 1
  - av: 20
    ca: 7
    flores: 1
---

# Solución: caminar la calle 7 hasta encontrar 20 flores (garantizadas)

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-04-veinte-flores-calle-7-garantizadas.md`](../ejercicios/ejercicio-04-veinte-flores-calle-7-garantizadas.md).

## Análisis

Como a lo sumo hay una flor por esquina y se garantiza que existen 20, alcanza con una variable `x` que cuente flores encontradas y un `mientras(x<20)` que avance esquina por esquina, tomando la flor si la hay. `Pos(1,7)` fija la calle y el `derecha` orienta al robot para recorrerla (avenida variable).

## Estrategia

1. Posicionar el robot en (1,7) y girar a la derecha.
2. Mientras `x<20`: si hay flor en la esquina, tomarla y contarla en `x`; avanzar.
3. Informar `x`.

## Código relacionado

```
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
    mientras(x<20)
      si(HayFlorEnLaEsquina)
        tomarFlor
        x:=x+1
      mover
    Informar(x)
  fin
variables
  robin:robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/capitulo-3-pregunta-04.ri`](../codigo/capitulo-3-pregunta-04.ri)

## Escenario de prueba

Cargar 20 esquinas de la calle 7 con 1 flor cada una (por ejemplo, avenidas 1 a 20). Probado con el intérprete de R-info: con flores en las avenidas 1 a 20 (ca=7), el programa informa `x = 20`.

## Casos límite

- Como todo `mientras` en R-info recién vuelve a evaluar su condición al terminar el cuerpo, si la flor número 20 está justo en la avenida 100 (la última de la calle), el `mover` final del cuerpo todavía se ejecuta antes de volver a chequear `x<20`, empujando al robot un paso más allá del límite de la ciudad. Este comportamiento es el mismo que usan los ejemplos de la propia teoría (2.9, 3.3) y no es un error introducido por este archivo en particular.
- La variable `y` está declarada pero no se usa; no afecta la ejecución.

## Errores frecuentes

- Olvidar que el enunciado garantiza la existencia de las 20 flores: sin esa garantía, este mismo patrón necesitaría además una condición de corte por `PosAv` (ver ejercicio 5).
- Tomar la flor sin contarla, o contarla sin tomarla primero.

## Complejidad

En el peor caso recorre toda la calle (100 esquinas): O(1) respecto al tamaño de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-04-veinte-flores-calle-7-garantizadas.md`](../ejercicios/ejercicio-04-veinte-flores-calle-7-garantizadas.md)
- Fuente original: [`../fuentes/Capitulo 3-Datos.pdf`](<../fuentes/Capitulo 3-Datos.pdf>)
- Código: [`../codigo/capitulo-3-pregunta-04.ri`](../codigo/capitulo-3-pregunta-04.ri)
