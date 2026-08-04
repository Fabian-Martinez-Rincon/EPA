---
id: "EPA-U02-EJ12-SOLUCION"
titulo: "Solución: depositar papel en las esquinas libres"
slug: "ejercicio-12-esquina-libre-depositar-papel"
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
  - "../ejercicios/ejercicio-12-esquina-libre-depositar-papel.md"
codigo_relacionado:
  - "../codigo/ejercicio-12.ri"
escenario_ciudad:
  - av: 5
    ca: 1
    flores: 0
    papeles: 1
  - av: 10
    ca: 1
    flores: 1
    papeles: 0
escenario_bolsa:
  flores: 0
  papeles: 10
---

# Solución: depositar papel en las esquinas libres

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-12-esquina-libre-depositar-papel.md`](../ejercicios/ejercicio-12-esquina-libre-depositar-papel.md).

## Análisis

Una esquina "libre" es una esquina sin flor y sin papel. El robot gira para orientarse a lo largo de las avenidas (recorre una calle completa, avenida 1 a 100) y, al llegar al final, salta a la próxima calle y repite — cubriendo así las 100 calles de la ciudad, no solo la primera. En cada esquina deposita un papel si está libre y todavía le queda alguno en la bolsa.

## Estrategia

1. Girar a la derecha para orientarse a lo largo de las avenidas.
2. Repetir 100 veces (una vez por calle):
   1. Repetir 99 veces: si la esquina actual está libre (sin flor y sin papel) y el robot tiene papel en la bolsa, depositarlo; avanzar.
   2. Repetir el mismo chequeo una vez más al llegar a la avenida 100 (sin avanzar: ya no hay a dónde ir en esta calle).
   3. Si no es la última calle, saltar al inicio de la siguiente con `Pos(1,PosCa+1)`.

## Código relacionado

```
programa antoja
areas
  ciudad:AreaC(1,1,100,100)
robots
  robot robot1
  comenzar
    derecha
    repetir 100
      repetir 99
        si (~HayPapelEnLaEsquina & ~HayFlorEnLaEsquina & HayPapelEnLaBolsa)
          depositarPapel
        mover
      si (~HayPapelEnLaEsquina & ~HayFlorEnLaEsquina & HayPapelEnLaBolsa)
        depositarPapel
      si(PosCa<100)
        Pos(1,PosCa+1)
  fin
variables
  R-Info: robot1
comenzar
  AsignarArea(R-Info,ciudad)
  Iniciar(R-Info,1,1)
fin
```

Código completo: [`../codigo/ejercicio-12.ri`](../codigo/ejercicio-12.ri)

## Corrección aplicada durante esta organización

El archivo histórico tenía tres problemas encadenados, los tres verificados con el intérprete de R-info de Academia-Fabo:

1. **Condición invertida:** la condición original era `HayPapelEnLaEsquina & HayFlorEnLaEsquina & HayPapelEnLaBolsa` — depositaba papel solo en esquinas que **ya tenían** flor y papel, justo lo opuesto de "esquina libre". Se negaron las dos primeras condiciones (`~HayPapelEnLaEsquina & ~HayFlorEnLaEsquina`).
2. **Se salía del área:** tras el único `derecha`, `mover` avanza en avenida creciente; con `repetir 100` el robot intentaba llegar a la avenida 101 (fuera de `AreaC(1,1,100,100)`), cortando la ejecución antes de terminar siquiera la calle 1. Se cambió a `repetir 99` (más el chequeo final sin `mover`, que ya estaba) para llegar exactamente a la avenida 100.
3. **Solo cubría una calle:** el `Pos(1,PosCa+1)` saltaba al inicio de la siguiente calle, pero nada volvía a ejecutar el recorrido para ella — el programa terminaba ahí. Se envolvió todo el bloque (recorrido de una calle + salto) en un `repetir 100` adicional (una vuelta por calle) y se corrigió la condición del salto a `PosCa<100` para que no intente saltar después de la última calle. También se quitó el `mover` final sobreviviente en el chequeo posterior al `repetir 99`, que habría vuelto a empujar al robot a la avenida 101 en cada calle una vez arreglado el punto 2.

Se verificó con el intérprete que, con distintos escenarios (ciudad vacía, esquinas ocupadas salteadas en varias calles, y una bolsa que se agota a mitad de camino), el robot recorre las 100 calles sin salirse del área y deposita únicamente en esquinas libres.

## Escenario de prueba

El escenario por defecto de este visor tiene esquinas ocupadas en (5,1) y (10,1) y una bolsa con 10 papeles: se puede observar que el robot las saltea y deposita en las esquinas libres de la calle 1 hasta agotar la bolsa. Para ver el recorrido completar varias calles, aumentar la bolsa (con 250 papeles alcanza para recorrer más de dos calles completas).

## Casos límite

- Esquina con flor pero sin papel (o viceversa): no se considera libre, no recibe depósito.
- Bolsa sin papeles: ninguna esquina recibe depósito de ahí en más, pero el robot sigue recorriendo el resto de la ciudad igual (el enunciado no pide detener el movimiento, solo el depósito).
- Última calle (100): el `si(PosCa<100)` evita el salto final, así que el robot no intenta salirse del área después de terminarla.

## Errores frecuentes

- Escribir la condición de "esquina libre" sin negar ambos `Hay...EnLaEsquina`, quedando invertida (el bug real que tenía este archivo).
- Usar `repetir 100` en vez de `repetir 99` para el eje que ya arrancó en la posición 1: al haber avanzado desde la esquina 1, alcanza con 99 movimientos más para llegar a la 100 — un `repetir 100` completo se pasa de largo.
- Saltar a la siguiente calle sin envolver el recorrido en un loop externo que lo repita: el salto por sí solo no hace que el recorrido "para todas las calles" vuelva a ejecutarse.

## Complejidad

Tiempo O(n) con n=10.000 esquinas (100 calles × 100 avenidas): recorre la ciudad completa una sola vez. Espacio O(1).

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-12-esquina-libre-depositar-papel.md`](../ejercicios/ejercicio-12-esquina-libre-depositar-papel.md)
- Código: [`../codigo/ejercicio-12.ri`](../codigo/ejercicio-12.ri)
