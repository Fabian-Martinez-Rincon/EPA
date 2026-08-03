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

```
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
        tomarFlor
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

## Nota de fidelidad con el enunciado

Este archivo histórico no implementa literalmente "el cuadrado (1,1)-(2,2)" del ejercicio 3 (lado 1), sino un cuadrado de lado 18 ubicado en otra posición, y recoge flor **y** papel en vez de solo papel como pide el enunciado. La técnica (perímetro cuadrado + recolección en cada esquina) es la correcta y generaliza bien a cualquier lado, pero no es una transcripción exacta del tamaño/posición pedidos. Se dejó el código sin modificar (no es un bug de una palabra como en otros ejercicios de esta unidad, sino una generalización del propio material histórico) — se documenta acá para que quede claro al leerlo junto al enunciado.

## Casos límite

- Esquina sin papel ni flor: `tomarFlor`/`tomarPapel` no tienen efecto (no hay nada que levantar).
- El segundo cuadrado se traza desde (30,30), no desde (1,1): si esa zona de la ciudad no tiene objetos cargados, el robot completa el recorrido sin recoger nada.

## Errores frecuentes

- Olvidar reposicionar (`Pos`) antes del segundo cuadrado y terminar dibujando un cuadrado superpuesto con el primero.
- Confundir el orden `mover` → `tomarFlor`/`tomarPapel` con levantar el objeto antes de entrar a la esquina.

## Complejidad

Dos recorridos de perímetro de longitud fija (4×18 pasos cada uno): O(1) respecto al tamaño de la ciudad, ya que el lado del cuadrado está fijo en el código.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-04-perimetro-cuadrado-con-papel.md`](../ejercicios/ejercicio-04-perimetro-cuadrado-con-papel.md)
- Fuente original: [`../fuentes/Capitulo 2-Algoritmos y Logica.pdf`](<../fuentes/Capitulo 2-Algoritmos y Logica.pdf>)
- Código: [`../codigo/ejercicio-04.ri`](../codigo/ejercicio-04.ri)
