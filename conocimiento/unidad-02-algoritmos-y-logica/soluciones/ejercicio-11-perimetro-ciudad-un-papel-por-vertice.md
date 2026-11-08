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
escenario_ciudad:
  - av: 1
    ca: 50
    flores: 1
    papeles: 1
  - av: 50
    ca: 100
    flores: 0
    papeles: 1
  - av: 100
    ca: 50
    flores: 0
    papeles: 1
  - av: 50
    ca: 1
    flores: 0
    papeles: 1
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

```rinfo
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

Poné flores y papeles en varias esquinas del borde, y algunos papeles en la bolsa. El robot da la vuelta completa levantando todo y deja un papel en cada uno de los cuatro vértices: (1,100), (100,100), (100,1) y (1,1).

## Casos límite

- Si la bolsa está vacía al llegar a un vértice, ese vértice queda sin papel. El `si(HayPapelEnLaBolsa)` evita el error de depositar sin tener.
- En un vértice que ya tenía papeles queda exactamente uno. El robot primero se los lleva todos con el `mientras`, y recién después deja el suyo.
- El vértice de partida (1,1) se resuelve fuera del bucle. El robot lo limpia al cerrar el cuarto lado y deposita ahí su último papel.

## Errores frecuentes

- Sumar (1,1) a la condición de adentro del bucle. El robot pasa por ahí al cerrar el cuarto lado, así que dejaría un papel adentro del bucle y otro en el `si` final: dos papeles en el mismo vértice.
- Depositar antes de levantar. Si el `mientras(HayPapelEnLaEsquina)` queda después del depósito, el robot se lleva su propio papel y el vértice termina vacío.
- Usar `si` en vez de `mientras` para levantar. Una esquina con dos flores se queda con una.

## Complejidad

Perímetro fijo de 4×99 esquinas: O(1) respecto al tamaño de la ciudad (perímetro fijo en 100×100).

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-11-perimetro-ciudad-un-papel-por-vertice.md`](../ejercicios/ejercicio-11-perimetro-ciudad-un-papel-por-vertice.md)
- Código: [`../codigo/ejercicio-11.ri`](../codigo/ejercicio-11.ri)
