---
id: "EPA-U06-EJ06-SOLUCION"
titulo: "Solución: recorrer avenidas con el número como parámetro"
slug: "ejercicio-06-recorrer-avenidas-con-numero-parametrizado"
tipo: "solucion"
unidad: 6
tema: "parametros-de-entrada"
subtemas:
  - "declaracion-de-parametros"
  - "comunicacion-entre-modulos"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 6-Parametros de Entrada.pdf"
    paginas: "1-20"
relacionados:
  - "../ejercicios/ejercicio-06-recorrer-avenidas-con-numero-parametrizado.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_6A"
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_6B"
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_6C"
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_6D"
---

# Solución: recorrer avenidas con el número como parámetro

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-06-recorrer-avenidas-con-numero-parametrizado.md`](../ejercicios/ejercicio-06-recorrer-avenidas-con-numero-parametrizado.md).

## Análisis

Recorrer una avenida es caminar desde la calle 1 hasta la 100 sin cambiar de avenida. El robot arranca mirando al norte, que es justo el eje de las avenidas, así que no hace falta ningún giro: alcanza con ubicarlo en `(numAv,1)` y avanzar 99 veces.

El proceso `RecorrerAvenida` recibe el número de avenida como parámetro de entrada (`E`). Las partes b, c y d no vuelven a escribir ese recorrido: lo invocan una vez por avenida, cambiando solo el valor que le pasan. Lo único que cambia entre las tres es desde qué avenida arrancan, cuántas veces repiten y de a cuánto avanza el número.

## Estrategia

**6.a:**

1. Declarar `proceso RecorrerAvenida(E numAv:numero)`.
2. Ubicar al robot en `(numAv,1)` con `Pos`.
3. Avanzar 99 veces: de la calle 1 a la 100.

**6.b, 6.c y 6.d:** guardar en una variable `av` la primera avenida y repetir "recorrerla y pasar a la siguiente":

| Parte | Primera avenida | Vueltas | Siguiente |
|---|---|---|---|
| 6.b | 1 | 100 | `av:=av+1` |
| 6.c | 5 | 11 | `av:=av+1` |
| 6.d | 2 | 50 | `av:=av+2` |

Las vueltas son la cantidad de avenidas a recorrer: de la 5 a la 15 hay 11, y entre la 2 y la 100 hay 50 pares.

## Código relacionado

### 6.a) — el proceso

```rinfo
programa parametros
procesos
  proceso RecorrerAvenida(E numAv:numero)
  comenzar
    Pos(numAv,1)
    repetir 99
      mover
  fin
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  variables
    av:numero
  comenzar
    av:=19
    RecorrerAvenida(av)
  fin
variables
  robin: robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-06/Cap6_Preg_6A`](../codigo/soluciones/capitulo-06/Cap6_Preg_6A)

### 6.b) — todas las avenidas

```rinfo
programa parametros
procesos
  proceso RecorrerAvenida(E numAv:numero)
  comenzar
    Pos(numAv,1)
    repetir 99
      mover
  fin
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  variables
    av:numero
  comenzar
    av:=1
    repetir 100
      RecorrerAvenida(av)
      av:=av+1
  fin
variables
  robin: robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-06/Cap6_Preg_6B`](../codigo/soluciones/capitulo-06/Cap6_Preg_6B)

### 6.c) — avenidas 5 a 15

```rinfo
programa parametros
procesos
  proceso RecorrerAvenida(E numAv:numero)
  comenzar
    Pos(numAv,1)
    repetir 99
      mover
  fin
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  variables
    av:numero
  comenzar
    av:=5
    repetir 11
      RecorrerAvenida(av)
      av:=av+1
  fin
variables
  robin: robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-06/Cap6_Preg_6C`](../codigo/soluciones/capitulo-06/Cap6_Preg_6C)

### 6.d) — avenidas pares

```rinfo
programa parametros
procesos
  proceso RecorrerAvenida(E numAv:numero)
  comenzar
    Pos(numAv,1)
    repetir 99
      mover
  fin
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  variables
    av:numero
  comenzar
    av:=2
    repetir 50
      RecorrerAvenida(av)
      av:=av+2
  fin
variables
  robin: robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-06/Cap6_Preg_6D`](../codigo/soluciones/capitulo-06/Cap6_Preg_6D)

## Escenario de prueba

Ciudad vacía: estos programas solo caminan. Fijate qué avenidas recorre cada uno. La 6.a hace solo la 19 y termina en (19,100); la 6.b recorre las 100 avenidas y termina en (100,100); la 6.c, de la 5 a la 15, y termina en (15,100); la 6.d, las 50 pares, y termina en (100,100). En las cuatro, cada avenida se camina entera, de la calle 1 a la 100.

## Casos límite

- La última vuelta de la 6.b y de la 6.d deja `av` en 101 y en 102, pero el proceso ya no se vuelve a invocar, así que el robot nunca intenta ir a una avenida fuera de la ciudad.
- Como el proceso empieza con `Pos(numAv,1)`, no importa dónde quedó el robot en la vuelta anterior: siempre arranca la avenida desde la calle 1.

## Errores frecuentes

- Girar con `derecha` antes de recorrer la avenida. El robot ya mira al norte, que es el eje de las avenidas. Con el giro terminaría recorriendo una calle.
- Contar los saltos entre avenidas en vez de las avenidas. De la 5 a la 15 hacen falta 11 vueltas, no 10: con 10 la avenida 15 queda sin recorrer.
- Volver a escribir el `repetir 99 mover` en las partes b, c y d. Funciona, pero el enunciado pide usar el proceso de la parte a: el recorrido de una avenida se escribe una sola vez.

## Complejidad

Cada invocación del proceso hace 99 pasos. La 6.a hace uno solo; la 6.b, 6.c y 6.d hacen 99 pasos por cada avenida que recorren.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-06-recorrer-avenidas-con-numero-parametrizado.md`](../ejercicios/ejercicio-06-recorrer-avenidas-con-numero-parametrizado.md)
- Código: [`../codigo/soluciones/capitulo-06/Cap6_Preg_6A`](../codigo/soluciones/capitulo-06/Cap6_Preg_6A), [`../codigo/soluciones/capitulo-06/Cap6_Preg_6B`](../codigo/soluciones/capitulo-06/Cap6_Preg_6B), [`../codigo/soluciones/capitulo-06/Cap6_Preg_6C`](../codigo/soluciones/capitulo-06/Cap6_Preg_6C), [`../codigo/soluciones/capitulo-06/Cap6_Preg_6D`](../codigo/soluciones/capitulo-06/Cap6_Preg_6D)
