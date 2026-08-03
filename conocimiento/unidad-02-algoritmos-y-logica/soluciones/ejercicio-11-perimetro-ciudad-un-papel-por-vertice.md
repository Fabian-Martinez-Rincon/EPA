---
id: "EPA-U02-EJ11-SOLUCION"
titulo: "Solución: recorrer el perímetro de la ciudad dejando un papel por vértice"
slug: "ejercicio-11-perimetro-ciudad-un-papel-por-vertice"
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
  - "../ejercicios/ejercicio-11-perimetro-ciudad-un-papel-por-vertice.md"
codigo_relacionado:
  - "../codigo/ejercicio-11.ri"
---

# Solución: recorrer el perímetro de la ciudad dejando un papel por vértice

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-11-perimetro-ciudad-un-papel-por-vertice.md`](../ejercicios/ejercicio-11-perimetro-ciudad-un-papel-por-vertice.md).

## Análisis

El perímetro se recorre con el patrón clásico `repetir 4 { repetir 99 mover; derecha }`, recogiendo flores y papeles en cada esquina intermedia. La parte específica de este ejercicio es reconocer los 4 vértices por coordenadas: tres de ellos se detectan dentro del recorrido (comparando `PosAv`/`PosCa` contra 1 y 100), y el cuarto — el vértice de partida (1,1) — se resuelve solo, porque el robot vuelve ahí naturalmente al completar el cuarto lado, y se lo maneja con un chequeo aparte después del `repetir 4`.

## Estrategia

1. Repetir 4 veces (una por lado del cuadrado): avanzar 99 veces recogiendo toda flor/papel de cada esquina, y si la esquina alcanzada es uno de los tres vértices no-iniciales, depositar un papel (si hay alguno en la bolsa); girar a la derecha al final del lado.
2. Al terminar los 4 lados el robot está de vuelta en (1,1): depositar ahí un papel si queda alguno en la bolsa.

## Código relacionado

```
programa antoja
areas
  ciudad:AreaC(1,1,100,100)
robots
  robot robot1
  comenzar
    repetir 4
      repetir 99
        mover
        mientras(HayFlorEnLaEsquina)
          tomarFlor
        mientras(HayPapelEnLaEsquina)
          tomarPapel
        si ((PosCa>=100)&(PosAv=1))|((PosAv=100)&(PosCa=100))|((PosAv=100)&(PosCa=1))
          si(HayPapelEnLaBolsa)
            depositarPapel
      derecha
    si(HayPapelEnLaBolsa)
      depositarPapel
  fin
variables
  R-Info: robot1
comenzar
  AsignarArea(R-Info,ciudad)
  Iniciar(R-Info,1,1)
fin
```

Código completo: [`../codigo/ejercicio-11.ri`](../codigo/ejercicio-11.ri)

## Escenario de prueba

Para ver el efecto completo conviene iniciar la simulación con flores/papeles en algunas esquinas del perímetro (los cuatro lados de la ciudad) y con la bolsa del robot vacía, para observar cómo va acumulando objetos y depositando papel en cada vértice a medida que los tiene disponibles.

## Casos límite

- Bolsa sin papeles al llegar a un vértice: ese vértice queda vacío (el `si(HayPapelEnLaBolsa)` evita el error de intentar depositar sin tener).
- Vértice (1,1): no se detecta con la condición dentro del bucle, se resuelve aparte al final porque el robot completa ahí su recorrido.

## Errores frecuentes

- Chequear el vértice de partida (1,1) dentro del bucle en vez de después: como el robot arranca ahí antes de moverse, ese chequeo temprano depositaría antes de haber recogido nada del resto del perímetro.
- Usar `mover` sin recoger flor/papel antes de evaluar si la esquina es vértice, dejando objetos sin levantar.

## Complejidad

Perímetro fijo de 4×99 esquinas: O(1) respecto al tamaño de la ciudad (perímetro fijo en 100×100).

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-11-perimetro-ciudad-un-papel-por-vertice.md`](../ejercicios/ejercicio-11-perimetro-ciudad-un-papel-por-vertice.md)
- Fuente original: [`../fuentes/Capitulo 2-Algoritmos y Logica.pdf`](<../fuentes/Capitulo 2-Algoritmos y Logica.pdf>)
- Código: [`../codigo/ejercicio-11.ri`](../codigo/ejercicio-11.ri)
