---
id: "EPA-U03-EJ02-SOLUCION"
titulo: "Solución: informar la cantidad de flores de la calle 44 sin modificar las esquinas"
slug: "ejercicio-02-informar-flores-calle-44-sin-modificar"
tipo: "solucion"
unidad: 3
tema: "datos-y-variables"
subtemas:
  - "variables"
  - "tipos-de-datos"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 3-Datos.pdf"
    paginas: "1-21"
relacionados:
  - "../ejercicios/ejercicio-02-informar-flores-calle-44-sin-modificar.md"
codigo_relacionado:
  - "../codigo/capitulo-3-pregunta-02.ri"
escenario_ciudad:
  - av: 50
    ca: 44
    flores: 3
    papeles: 0
---

# Solución: informar la cantidad de flores de la calle 44 sin modificar las esquinas

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-02-informar-flores-calle-44-sin-modificar.md`](../ejercicios/ejercicio-02-informar-flores-calle-44-sin-modificar.md).

## Análisis

`Pos(1,44)` fija la calle en 44; el `derecha` orienta al robot para recorrer esa calle (avenida variable, calle fija), tal como pide el enunciado. El patrón `repetir 99 {...; mover} + chequeo final` (el mismo usado en el ejemplo 3.7 de la teoría) cubre las 100 esquinas de la calle (avenidas 1 a 100). En cada esquina se toman todas las flores contándolas en `x`, y luego se depositan de nuevo con `mientras(HayFlorEnLaBolsa) depositarFlor` antes de avanzar, de modo que la esquina queda exactamente como estaba.

## Estrategia

1. Posicionar el robot en (1,44) y girar a la derecha para orientarse a lo largo de la calle.
2. Repetir 99 veces: tomar todas las flores de la esquina actual contándolas en `x`, depositarlas de nuevo, avanzar.
3. Repetir el mismo procesamiento (sin avanzar) para la esquina final, la avenida 100.
4. Informar `x`.

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
    Pos(1,44)
    x:=0
    derecha
    repetir 99
      mientras(HayFlorEnLaEsquina)
        tomarFlor
        x:=x+1
      mientras (HayFlorEnLaBolsa)
        depositarFlor
      mover
    mientras(HayFlorEnLaEsquina)
      tomarFlor
      x:=x+1
    mientras(HayFlorEnLaBolsa)
      depositarFlor
    Informar(x)
  fin
variables
  robin:robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/capitulo-3-pregunta-02.ri`](../codigo/capitulo-3-pregunta-02.ri)

## Este código resuelve la variante 2

El enunciado pide dos cosas: contar las flores llevándoselas, y contarlas sin tocar el contenido de cada esquina. Acá está resuelta la segunda. Después de contar las flores de una esquina, el robot se las devuelve con `mientras(HayFlorEnLaBolsa) depositarFlor`.

Si querés la variante 1, borrá los dos `mientras(HayFlorEnLaBolsa) depositarFlor`. El robot cuenta igual y se queda con todo en la bolsa.

La variable `y` se declara y nunca se usa. No rompe nada, pero tampoco hace falta.

## Escenario de prueba

Cargá flores en algunas esquinas de la calle 44 antes de arrancar. Con 3 flores en la avenida 50 y el resto de la calle vacía, el robot informa `3` y deja esa esquina con las mismas 3 flores que tenía.

## Casos límite

- Calle 44 sin ninguna flor: informa `0` y no deposita nada.
- Si arrancás la simulación con flores en la bolsa, el robot las suelta todas en la avenida 1, la primera esquina que pisa. La cuenta sigue bien, pero la calle queda modificada. Para probar este ejercicio la bolsa va vacía.

## Errores frecuentes

- Contar con `si(HayFlorEnLaEsquina)` en vez de `mientras`. Si la esquina tiene 3 flores, te llevás una sola y contás una sola.
- Devolver las flores después del `mover`. Van a parar a la esquina siguiente, así que la calle termina distinta de como estaba.
- Invertir los argumentos de `Pos`. `Pos(44,1)` deja al robot en la avenida 44 de la calle 1, y el `derecha` lo manda a recorrer la calle 1 hasta salirse de la ciudad.

## Complejidad

Recorrido fijo de 100 esquinas (una calle completa): O(1) respecto al tamaño de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-02-informar-flores-calle-44-sin-modificar.md`](../ejercicios/ejercicio-02-informar-flores-calle-44-sin-modificar.md)
- Código: [`../codigo/capitulo-3-pregunta-02.ri`](../codigo/capitulo-3-pregunta-02.ri)
