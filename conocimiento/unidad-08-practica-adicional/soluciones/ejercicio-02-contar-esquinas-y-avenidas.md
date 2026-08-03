---
id: "EPA-U08-EJ02-SOLUCION"
titulo: "Solución: contar esquinas con 20 flores y avenidas con menos de 60 papeles"
slug: "ejercicio-02-contar-esquinas-y-avenidas"
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
  - "../ejercicios/ejercicio-02-contar-esquinas-y-avenidas.md"
codigo_relacionado:
  - "../codigo/ejercicio-02.ri"
escenario_ciudad:
  - av: 1
    ca: 1
    flores: 20
  - av: 1
    ca: 2
    papeles: 1
---

# Solución: contar esquinas con 20 flores y avenidas con menos de 60 papeles

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-02-contar-esquinas-y-avenidas.md`](../ejercicios/ejercicio-02-contar-esquinas-y-avenidas.md).

## Análisis

Como no se puede alterar el contenido de las esquinas, "mirar sin modificar" se resuelve tomando todo lo que hay y depositándolo de nuevo inmediatamente (`ContarFloresEsquina`/`ContarPapelesEsquina`). `ProcesarAvenida` recorre una avenida completa acumulando ambos conteos por esquina y decide, al final de la avenida, si tuvo menos de 60 papeles en total.

## Estrategia

1. `ContarFloresEsquina(ES flores)` / `ContarPapelesEsquina(ES papeles)`: toman todo lo que hay, cuentan cuánto era, y lo vuelven a depositar — la esquina queda igual que antes.
2. `ProcesarAvenida(ES esquinas20, ES avenidasMenos60)`: recorre las 100 esquinas de la avenida actual, sumando 1 a `esquinas20` por cada esquina con exactamente 20 flores, y acumulando el total de papeles de la avenida para compararlo con 60 al final.
3. Driver: repetir 99 veces (avenidas 1 a 99) llamando a `ProcesarAvenida` y saltando a la próxima avenida con `Pos`, más una vez más para la avenida 100; al final, informar los dos contadores acumulados.

## Código relacionado

```
programa EjAdic2

procesos

  {Cuenta flores de la esquina SIN modificar (toma y repone)}
  proceso ContarFloresEsquina (ES flores: numero)
  variables
    aux: numero
  comenzar
    aux := 0
    mientras HayFlorEnLaEsquina
      tomarFlor
      aux := aux + 1
    repetir aux
      depositarFlor
    flores := flores + aux
  fin

  {Cuenta papeles de la esquina SIN modificar (toma y repone)}
  proceso ContarPapelesEsquina (ES papeles: numero)
  variables
    aux: numero
  comenzar
    aux := 0
    mientras HayPapelEnLaEsquina
      tomarPapel
      aux := aux + 1
    repetir aux
      depositarPapel
    papeles := papeles + aux
  fin

  proceso ProcesarAvenida (ES esquinas20: numero; ES avenidasMenos60: numero)
  variables
    papelesAvenida, floresEsq, papelesEsq: numero
  comenzar
    papelesAvenida := 0

    repetir 99
      floresEsq := 0
      ContarFloresEsquina(floresEsq)
      si (floresEsq = 20)
        esquinas20 := esquinas20 + 1

      papelesEsq := 0
      ContarPapelesEsquina(papelesEsq)
      papelesAvenida := papelesAvenida + papelesEsq

      mover

    floresEsq := 0
    ContarFloresEsquina(floresEsq)
    si (floresEsq = 20)
      esquinas20 := esquinas20 + 1

    papelesEsq := 0
    ContarPapelesEsquina(papelesEsq)
    papelesAvenida := papelesAvenida + papelesEsq

    si (papelesAvenida < 60)
      avenidasMenos60 := avenidasMenos60 + 1
  fin


areas
  ciudad: AreaC(1,1,100,100)

robots
  robot robot1
  variables
    totalEsquinas20, totalAvenidasMenos60: numero
  comenzar
    totalEsquinas20 := 0
    totalAvenidasMenos60 := 0

    repetir 99
      ProcesarAvenida(totalEsquinas20, totalAvenidasMenos60)
      Pos(PosAv + 1, 1)

    ProcesarAvenida(totalEsquinas20, totalAvenidasMenos60)

    Informar(totalEsquinas20)
    Informar(totalAvenidasMenos60)
  fin

variables
  R-info: robot1

comenzar
  AsignarArea(R-info, ciudad)
  Iniciar(R-info, 1, 1)
fin
```

Código completo: [`../codigo/ejercicio-02.ri`](../codigo/ejercicio-02.ri)

## Corrección aplicada durante esta organización

El driver tenía `repetir 9` para el bloque comentado como "Avenidas 1 a 99", cuando debía ser `repetir 99` — con `9` el programa solo alcanzaba a procesar 10 de las 100 avenidas (el comentario "Avenida 100" quedaba resolviendo en realidad la avenida 10). Se corrigió el número, sin tocar el resto de la lógica.

## Escenario de prueba

Probado con el intérprete de R-info de Academia-Fabo con una esquina cargada con 20 flores y otra con 1 papel: terminó en 10045 eventos e informó `1` esquina con 20 flores y `100` avenidas con menos de 60 papeles (esperable, dado que casi ninguna avenida llega a 60 papeles en un escenario de prueba con tan pocos objetos cargados).

## Casos límite

- Una esquina con exactamente 20 flores cuenta; con 19 o 21 no.
- Una avenida con exactamente 60 papeles NO cuenta como "menos de 60" (`<`, no `<=`).
- El proceso de conteo debe reponer exactamente la misma cantidad que tomó, para no alterar la esquina — por eso `repetir aux: depositarFlor/depositarPapel` en vez de un valor fijo.

## Errores frecuentes

- Repetir 9 en vez de 99 en el driver (el bug real corregido en esta organización).
- Usar `<=` en vez de `<` para "menos de 60 papeles".
- Olvidar reponer lo tomado en `ContarFloresEsquina`/`ContarPapelesEsquina`, violando la restricción de "no modificar" las esquinas.

## Complejidad

O(n) en el tamaño de la ciudad: cada esquina se visita una vez, con trabajo constante por esquina.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-02-contar-esquinas-y-avenidas.md`](../ejercicios/ejercicio-02-contar-esquinas-y-avenidas.md)
- Fuente original: [`../fuentes/Ejercicios Adicionales.pdf`](<../fuentes/Ejercicios Adicionales.pdf>)
- Código: [`../codigo/ejercicio-02.ri`](../codigo/ejercicio-02.ri)
- Versión guiada: [`../practica-guiada.md`](../practica-guiada.md)
