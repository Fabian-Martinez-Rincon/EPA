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

```
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

Probado con el intérprete de R-info de Academia-Fabo cargando flores/papeles en algunas esquinas puntuales (por ejemplo, esquina (1,1) con 2 flores y esquina (2,5) con 1 papel): terminó en 204 eventos e informó `1` (a lo sumo 45 flores) en las 100 avenidas, como es esperable si ninguna avenida individual llega a acumular más de 45 flores antes de su esquina vacía.

## Casos límite

- Una avenida sin ninguna flor ni papel desde el inicio: el `mientras` externo no entra nunca, `totalFlores` queda en 0, se informa `1`.
- Una avenida con más de 45 flores antes de la esquina vacía: se informa `0`.
- La nota del propio enunciado aclara la equivalencia "a lo sumo" = "máximo" = `<=`, no `<`.

## Errores frecuentes

- Usar `<` en vez de `<=` en `InformarAvenida`, excluyendo el caso borde de exactamente 45 flores.
- Tomar también los papeles dentro de `RecorrerAvenidaHastaVacia` (el enunciado solo pide contar flores; los papeles se usan nada más para decidir si la esquina está vacía).
- Repetir 100 veces en vez de 99+1: reposicionar con `Pos(PosAv+1,1)` en la avenida 100 llevaría al robot fuera del área (avenida 101).

## Complejidad

O(n) en el tamaño de la ciudad: cada esquina de las 100 avenidas se visita una vez.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-01-recorrer-avenidas-hasta-esquina-vacia.md`](../ejercicios/ejercicio-01-recorrer-avenidas-hasta-esquina-vacia.md)
- Código: [`../codigo/ejercicio-01.ri`](../codigo/ejercicio-01.ri)
- Versión guiada con animación: [`../practica-guiada.md`](../practica-guiada.md)
