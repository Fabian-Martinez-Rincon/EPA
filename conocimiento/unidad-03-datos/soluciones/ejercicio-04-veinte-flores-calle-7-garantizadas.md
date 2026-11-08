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

Poné una flor en cada una de las avenidas 1 a 20 de la calle 7. El robot informa `20` y queda parado en la avenida 21. El `mover` es la última instrucción del cuerpo, así que se ejecuta una vez más antes de que el `mientras` vuelva a mirar la condición.

## Casos límite

- Si la calle no tiene las 20 flores, este programa no termina bien. `x<20` nunca se vuelve falso, el robot sigue avanzando y al querer pasar la avenida 100 se sale de la ciudad: error de ejecución, sin informar nada. El enunciado garantiza las 20 justamente para que eso no pase. El ejercicio 5 es la versión que aguanta el otro caso.
- Lo mismo pasa si la flor número 20 está justo en la avenida 100. El robot la toma, `x` llega a 20, pero el `mover` que viene después ya no tiene a dónde ir.

## Errores frecuentes

- Tomar la flor sin contarla. `x` se queda en 0 y el robot camina hasta salirse de la ciudad.
- Poner el `mover` adentro del `si(HayFlorEnLaEsquina)`. El robot sólo avanza cuando encuentra flor, así que en la primera esquina vacía se queda clavado para siempre.

## Complejidad

En el peor caso recorre toda la calle (100 esquinas): O(1) respecto al tamaño de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-04-veinte-flores-calle-7-garantizadas.md`](../ejercicios/ejercicio-04-veinte-flores-calle-7-garantizadas.md)
- Código: [`../codigo/capitulo-3-pregunta-04.ri`](../codigo/capitulo-3-pregunta-04.ri)
