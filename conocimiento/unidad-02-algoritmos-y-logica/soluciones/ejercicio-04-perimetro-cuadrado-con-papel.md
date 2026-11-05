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
  - av: 30
    ca: 30
    flores: 1
    papeles: 1
  - av: 30
    ca: 48
    flores: 2
    papeles: 0
  - av: 48
    ca: 48
    flores: 0
    papeles: 2
  - av: 48
    ca: 30
    flores: 1
    papeles: 1
---

# Solución: modificar el perímetro del cuadrado para recoger papel

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-04-perimetro-cuadrado-con-papel.md`](../ejercicios/ejercicio-04-perimetro-cuadrado-con-papel.md).

## Análisis

Recorrer un perímetro cuadrado en R-info es "avanzar N pasos, girar a la derecha", repetido 4 veces. El archivo histórico hace esto dos veces con lado 18 (no con lado 1, como el cuadrado literal (1,1)-(2,2) del ejercicio 3): primero un perímetro sin recoger nada, y después — tras reposicionarse en (30,30) — un segundo perímetro del mismo tamaño recogiendo flor y papel en cada esquina.

## Estrategia

1. Recorrer un cuadrado de lado 18 (`repetir 4 { repetir 18 mover; derecha }`) sin acciones adicionales, como demostración del patrón base.
2. Reposicionarse en (30,30) y recorrer un segundo cuadrado igual, esta vez con `tomarFlor` y `tomarPapel` en cada esquina intermedia.

## Código relacionado

```rinfo
programa robin
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  comenzar
    repetir 4
      repetir 18
        mover
      derecha
    Pos(30,30)
    repetir 4
      repetir 18
        mover
        si HayFlorEnLaEsquina
          tomarFlor
        si HayPapelEnLaEsquina
          tomarPapel
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

## El cuadrado del código es más grande que el del enunciado

El enunciado pide el cuadrado de lado 1 que va de (1,1) a (2,2). El código traza dos cuadrados de lado 18: el primero arranca en (1,1) y no recoge nada, el segundo va de (30,30) a (48,48) levantando flor y papel en cada esquina, cuando el enunciado solo pide papel. La técnica es la misma. Si cambiás los dos `repetir 18` por `repetir 1`, tenés el cuadrado del enunciado.

## Casos límite

- Esquina sin nada: por eso van los `si`. En R-Info, `tomarFlor` o `tomarPapel` en una esquina vacía corta el programa con un error.
- Poné los objetos entre (30,30) y (48,48). El primer cuadrado no recoge nada, es solo el patrón base.

## Errores frecuentes

- Olvidar el `Pos(30,30)`. Los dos cuadrados se superponen y el segundo recorre las mismas esquinas que el primero.
- Levantar antes de mover. Si ponés `tomarFlor` arriba del `mover`, buscás en la esquina de la que ya estás saliendo y te salteás la última de cada lado.

## Complejidad

Dos recorridos de perímetro de longitud fija (4×18 pasos cada uno): O(1) respecto al tamaño de la ciudad, ya que el lado del cuadrado está fijo en el código.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-04-perimetro-cuadrado-con-papel.md`](../ejercicios/ejercicio-04-perimetro-cuadrado-con-papel.md)
- Código: [`../codigo/ejercicio-04.ri`](../codigo/ejercicio-04.ri)
