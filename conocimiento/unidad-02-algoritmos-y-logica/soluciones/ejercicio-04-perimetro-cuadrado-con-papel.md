---
id: "EPA-U02-EJ04-SOLUCION"
titulo: "Solución: modificar el perímetro del cuadrado para recoger papel"
slug: "ejercicio-04-perimetro-cuadrado-con-papel"
tipo: "solucion"
unidad: 2
tema: "algoritmos-logica-y-r-info"
subtemas:
  - "estructuras-de-control"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 2-Algoritmos y Logica.pdf"
    paginas: "1-30"
relacionados:
  - "../ejercicios/ejercicio-04-perimetro-cuadrado-con-papel.md"
codigo_relacionado:
  - "../codigo/ejercicio-04.ri"
escenario_ciudad:
  - av: 1
    ca: 1
    papeles: 1
  - av: 1
    ca: 2
    flores: 1
  - av: 2
    ca: 2
    papeles: 3
  - av: 2
    ca: 1
    flores: 1
    papeles: 1
---

# Solución: modificar el perímetro del cuadrado para recoger papel

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-04-perimetro-cuadrado-con-papel.md`](../ejercicios/ejercicio-04-perimetro-cuadrado-con-papel.md).

## Análisis

Recorrer un perímetro en R-info es repetir 4 veces "avanzar un lado y girar a la derecha". Como el cuadrado va de (1,1) a (2,2), cada lado mide un solo paso. Las esquinas del recorrido son exactamente los cuatro vértices: (1,1), (1,2), (2,2) y (2,1).

## Estrategia

1. En cada vértice, antes de salir, preguntar si hay papel y tomar uno si lo hay.
2. Avanzar un paso y girar a la derecha.
3. Repetir 4 veces. El robot vuelve a (1,1) mirando al norte.

## Código relacionado

```rinfo
programa robin
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  comenzar
    repetir 4
      si HayPapelEnLaEsquina
        tomarPapel
      mover
      derecha
  fin
variables
  pop:robot1
comenzar
  AsignarArea(pop,ciudad)
  Iniciar(pop,1,1)
fin
```

Código completo: [`../codigo/ejercicio-04.ri`](../codigo/ejercicio-04.ri)

## Escenario de prueba

Con papel en (1,1), (2,2) y (2,1), y flores en (1,2) y (2,1), el robot toma un papel en (1,1), uno en (2,2) (de los 3 que hay) y uno en (2,1). Las flores no se tocan: el enunciado pide solo papel. Termina en (1,1) con 3 papeles en la bolsa.

## Casos límite

- Esquina sin papel: por eso va el `si`. En R-Info, `tomarPapel` en una esquina sin papel corta el programa con un error.
- Esquina con varios papeles: se toma uno solo, como pide el enunciado.

## Errores frecuentes

- Preguntar después del `mover`. Si ponés el `si` abajo del `mover`, la esquina de salida (1,1) se revisa recién al final, cuando el robot vuelve: funciona igual, pero si después agregás pasos al recorrido es fácil olvidarla.
- Usar `mientras HayPapelEnLaEsquina` en vez de `si`: levanta todos los papeles de la esquina, no uno.

## Complejidad

Cuatro pasos y cuatro preguntas: O(1), el recorrido no depende del tamaño de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-04-perimetro-cuadrado-con-papel.md`](../ejercicios/ejercicio-04-perimetro-cuadrado-con-papel.md)
- Código: [`../codigo/ejercicio-04.ri`](../codigo/ejercicio-04.ri)
