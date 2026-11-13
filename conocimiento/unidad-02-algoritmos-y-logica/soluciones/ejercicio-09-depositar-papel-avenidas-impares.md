---
id: "EPA-U02-EJ09-SOLUCION"
titulo: "Solución: depositar papel en las avenidas impares de la calle 17"
slug: "ejercicio-09-depositar-papel-avenidas-impares"
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
  - "../ejercicios/ejercicio-09-depositar-papel-avenidas-impares.md"
codigo_relacionado:
  - "../codigo/ejercicio-09.ri"
escenario_bolsa:
  flores: 0
  papeles: 50
---

# Solución: depositar papel en las avenidas impares de la calle 17

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-09-depositar-papel-avenidas-impares.md`](../ejercicios/ejercicio-09-depositar-papel-avenidas-impares.md).

## Análisis

Las avenidas impares de la calle 17 son la 1, 3, 5, ..., 99: cincuenta en total. Si el robot arranca en la avenida 1 mirando al este, basta con depositar y avanzar dos esquinas, así siempre cae en una impar sin tener que calcular nada. Después de la avenida 99 queda un último paso hasta la 100, que es donde el enunciado dice que termina el recorrido.

## Estrategia

1. Ubicar al robot en (1,17) y girarlo hacia el este.
2. Repetir 49 veces: depositar un papel (si queda alguno en la bolsa) y avanzar dos esquinas. Eso cubre de la avenida 1 a la 97 y deja al robot en la 99.
3. Depositar en la 99 y dar el último paso hasta (100,17).

## Código relacionado

```rinfo
programa antoja
areas
  ciudad:AreaC(1,1,100,100)
robots
  robot robot1
  comenzar
    Pos(1,17)
    derecha
    repetir 49
      si HayPapelEnLaBolsa
        depositarPapel
      mover
      mover
    si HayPapelEnLaBolsa
      depositarPapel
    mover
  fin
variables
  R-Info: robot1
comenzar
  AsignarArea(R-Info,ciudad)
  Iniciar(R-Info,1,1)
fin
```

Código completo: [`../codigo/ejercicio-09.ri`](../codigo/ejercicio-09.ri)

## Escenario de prueba

Con 50 papeles en la bolsa, el robot deja uno en cada avenida impar de la calle 17, de la 1 a la 99, y termina en (100,17) con la bolsa vacía. Con menos papeles, deposita mientras le queden y sigue caminando igual hasta la 100.

## Casos límite

- La avenida 1 también es impar: el primer depósito se hace antes de moverse.
- La avenida 99 queda fuera del `repetir` porque después de ella hay un solo paso, no dos. Si la metés adentro con un `repetir 50`, el segundo `mover` de la última vuelta saca al robot de la ciudad.

## Errores frecuentes

- Escribir `HayFlorEnLaBolsa` y `depositarFlor`. Acá se piden papeles, y la calle 17 queda sin nada.
- Olvidar el `derecha`. El robot arranca mirando al norte y sube por la avenida 1 en vez de recorrer la calle 17.
- Saltar con `Pos(PosAv+2,17)`: así el robot nunca pasa por la avenida 100 y el recorrido termina en la 99, no donde pide el enunciado.

## Complejidad

99 pasos fijos: O(1) respecto al tamaño de la ciudad (el rango de avenidas está fijo en el código).

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-09-depositar-papel-avenidas-impares.md`](../ejercicios/ejercicio-09-depositar-papel-avenidas-impares.md)
- Código: [`../codigo/ejercicio-09.ri`](../codigo/ejercicio-09.ri)
