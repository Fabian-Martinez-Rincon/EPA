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
estado: "parcial"
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

Una esquina "libre" es una esquina sin flor y sin papel. El robot gira para orientarse a lo largo de una calle y avanza 100 veces, depositando un papel en cada esquina libre que encuentra, siempre que le queden papeles en la bolsa.

## Estrategia

1. Girar a la derecha para orientarse a lo largo de la calle.
2. Repetir 100 veces: si la esquina actual está libre (sin flor y sin papel) y el robot tiene papel en la bolsa, depositarlo; avanzar.
3. Repetir el mismo chequeo una vez más al llegar al final de la calle.

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
      si (~HayPapelEnLaEsquina & ~HayFlorEnLaEsquina & HayPapelEnLaBolsa)
        depositarPapel
      mover
    si (~HayPapelEnLaEsquina & ~HayFlorEnLaEsquina & HayPapelEnLaBolsa)
      depositarPapel
      mover
    si(PosCa<99)
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

La condición original era `HayPapelEnLaEsquina & HayFlorEnLaEsquina & HayPapelEnLaBolsa` — es decir, depositaba papel solo en esquinas que **ya tenían** flor y papel, justo lo opuesto de "esquina libre". Se negaron las dos primeras condiciones (`~HayPapelEnLaEsquina & ~HayFlorEnLaEsquina`) para que el depósito ocurra donde el enunciado pide: esquinas sin flor y sin papel.

## Alcance no corregido: solo recorre una calle, y se pasa de largo

Después del `repetir 100` el código hace `Pos(1,PosCa+1)` para saltar al inicio de la siguiente calle, pero el programa termina ahí (`fin`) sin repetir el recorrido para esa nueva calle — es decir, tal como está el archivo histórico, solo cubre la calle 1, no "todas las calles" como pide el enunciado. A diferencia del bug de la condición (un cambio de una línea, ya corregido arriba), esto requeriría envolver todo el bloque en un `repetir 99` adicional, un cambio de estructura mayor — se documenta acá en vez de reescribirlo, siguiendo el mismo criterio que con `ejercicio-08.ri`/`ejercicio-10.ri` (no inventar una solución nueva sobre contenido `origen: convertido`).

Además, probando este archivo contra el intérprete de R-info construido para Academia-Fabo apareció un segundo problema, independiente del anterior: el robot gira una vez (queda orientado hacia avenidas crecientes, partiendo de la avenida 1) y el `repetir 100` lo hace intentar moverse 100 veces, lo que lo lleva a la avenida 101 — fuera del área válida (1 a 100) — y corta la ejecución antes de terminar siquiera la calle 1. Tendría que ser `repetir 99` para llegar exactamente a la avenida 100. No se corrigió por el mismo motivo que el punto anterior (es parte del mismo problema de alcance/estructura, no un fix de una palabra suelta) — se deja documentado porque es información nueva que no se había detectado en la revisión manual del enunciado, solo se hizo evidente al ejecutar el código.

## Escenario de prueba

Para ver el efecto conviene iniciar la simulación con la calle 1 mezclando esquinas libres y esquinas con flor/papel ya puestos, y con papeles en la bolsa del robot: se debería ver depósito solo en las esquinas libres de esa calle.

## Casos límite

- Esquina con flor pero sin papel (o viceversa): no se considera libre, no recibe depósito.
- Bolsa sin papeles: ninguna esquina recibe depósito, aunque esté libre.

## Errores frecuentes

- Escribir la condición de "esquina libre" sin negar ambos `Hay...EnLaEsquina`, quedando invertida (el bug real que tenía este archivo).
- Asumir que el `Pos(1,PosCa+1)` final implica que el recorrido continúa para todas las calles — como se explica arriba, no es así en este archivo.

## Complejidad

Un recorrido de 100 esquinas (una calle completa): O(1) respecto al tamaño de la ciudad para esa única calle; no aplica a "todas las calles" porque el archivo no las recorre.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-12-esquina-libre-depositar-papel.md`](../ejercicios/ejercicio-12-esquina-libre-depositar-papel.md)
- Fuente original: [`../fuentes/Capitulo 2-Algoritmos y Logica.pdf`](<../fuentes/Capitulo 2-Algoritmos y Logica.pdf>)
- Código: [`../codigo/ejercicio-12.ri`](../codigo/ejercicio-12.ri)
