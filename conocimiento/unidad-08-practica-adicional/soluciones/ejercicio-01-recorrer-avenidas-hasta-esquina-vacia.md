---
id: "EPA-U08-EJ01-SOLUCION"
titulo: "Solución: recorrer todas las avenidas hasta esquina vacía"
slug: "ejercicio-01-recorrer-avenidas-hasta-esquina-vacia"
tipo: "solucion"
unidad: 8
tema: "practica-adicional"
subtemas:
  - "modularizacion"
nivel: "intermedio"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Ejercicios Adicionales.pdf"
    paginas: "1-2"
relacionados:
  - "../ejercicios/ejercicio-01-recorrer-avenidas-hasta-esquina-vacia.md"
codigo_relacionado:
  - "../codigo/ejercicio-01.ri"
escenario_ciudad:
  - av: 1
    ca: 1
    flores: 2
  - av: 2
    ca: 5
    papeles: 1
---

# Solución: recorrer todas las avenidas hasta esquina vacía

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-01-recorrer-avenidas-hasta-esquina-vacia.md`](../ejercicios/ejercicio-01-recorrer-avenidas-hasta-esquina-vacia.md).

## Análisis

Se modulariza en dos procesos: uno que recorre una avenida completa contando flores hasta la esquina vacía (parámetro `ES` porque el conteo tiene que "salir" del proceso), y otro que decide qué informar a partir de ese conteo (parámetro `E`, solo entra). El driver repite esto para las 100 avenidas, reposicionándose con `Pos` entre una y la siguiente.

## Estrategia

1. `RecorrerAvenidaHastaVacia(ES totalFlores)`: mientras la esquina tenga flor o papel, si tiene flor la toma y suma 1 a `totalFlores`, y avanza. Se detiene apenas la esquina no tiene ni flor ni papel.
2. `InformarAvenida(E floresAvenida)`: informa `1` si `floresAvenida <= 45`, si no informa `0`.
3. Driver: repetir 99 veces (avenidas 1 a 99) reiniciar el contador, recorrer, informar, y saltar a la avenida siguiente con `Pos(PosAv+1,1)`; después repetir una vez más para la avenida 100 (sin el salto final).

## Código relacionado

```rinfo
programa Cap7Ejercicio1

procesos
  proceso RecorrerAvenidaHastaVacia(ES totalFlores: numero)
  comenzar
    mientras (HayFlorEnLaEsquina | HayPapelEnLaEsquina)
      mientras HayFlorEnLaEsquina
        tomarFlor
        totalFlores := totalFlores + 1
      mover
  fin

  proceso InformarAvenida (E floresAvenida: numero)
  comenzar
    si (floresAvenida <= 45)
      Informar(1)
    sino
      Informar(0)
  fin


areas
  ciudad: AreaC(1,1,100,100)

robots
  robot robot1
  variables
    floresAvenida: numero
  comenzar
    repetir 99
      floresAvenida := 0
      RecorrerAvenidaHastaVacia(floresAvenida)
      InformarAvenida(floresAvenida)
      Pos(PosAv + 1, 1)

    RecorrerAvenidaHastaVacia(floresAvenida)
    InformarAvenida(floresAvenida)
  fin

variables
  R-info: robot1

comenzar
  AsignarArea(R-info, ciudad)
  Iniciar(R-info, 1, 1)
fin
```

Código completo: [`../codigo/ejercicio-01.ri`](../codigo/ejercicio-01.ri)

## Escenario de prueba

El escenario carga 2 flores en (1,1) y 1 papel en (2,5). Salen 100 `Informar`, todos con el valor `1`: la avenida 1 junta 2 flores antes de llegar a su esquina vacía y las otras 99 no juntan ninguna. Dos y cero están los dos por debajo de 45.

## Casos límite

- Una avenida vacía desde la calle 1: el `mientras` externo no entra nunca, `totalFlores` queda en 0 y se informa `1`.
- Con exactamente 45 flores se informa `1`. Con 46 se informa `0`. "A lo sumo 45" incluye al 45, por eso la comparación es `<=`.
- Si una avenida no tuviera ninguna esquina vacía, el robot llegaría a la calle 100 y el `mover` siguiente lo sacaría de la ciudad. El enunciado garantiza que siempre hay una.

## Errores frecuentes

- Usar `<` en vez de `<=` y dejar afuera el caso de exactamente 45 flores.
- Sumar los papeles a `totalFlores`. Se cuentan solo flores; los papeles están únicamente para decidir dónde termina la avenida.
- Meter el `Pos(PosAv+1,1)` en un `repetir 100`. Al terminar la avenida 100 el salto apunta a la 101 y el programa corta con `Pos(101,1) está fuera del área`. Por eso el ciclo repite 99 veces y la última avenida se recorre aparte, sin salto.

## Complejidad

O(n) en el tamaño de la ciudad: cada esquina de las 100 avenidas se visita una vez.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-01-recorrer-avenidas-hasta-esquina-vacia.md`](../ejercicios/ejercicio-01-recorrer-avenidas-hasta-esquina-vacia.md)
- Código: [`../codigo/ejercicio-01.ri`](../codigo/ejercicio-01.ri)
- Versión guiada con animación: [`../practica-guiada.md`](../practica-guiada.md)
