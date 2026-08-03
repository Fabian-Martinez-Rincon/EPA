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
---

# Solución: depositar papel en las avenidas impares de la calle 17

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-09-depositar-papel-avenidas-impares.md`](../ejercicios/ejercicio-09-depositar-papel-avenidas-impares.md).

## Análisis

En vez de moverse esquina por esquina, el código salta directamente de avenida impar en avenida impar con `Pos(PosAv+2,17)`, que reposiciona al robot sin necesidad de calcular `PosAv mod 2`. Al partir de la avenida 1 (impar) y sumar 2 en cada paso, todas las posiciones visitadas son impares por construcción.

## Estrategia

1. Reposicionar el robot en (1,17).
2. Repetir 49 veces: saltar a la siguiente avenida impar (`Pos(PosAv+2,17)`) y, si hay papel en la bolsa, depositarlo.

## Código relacionado

```
programa antoja
areas
  ciudad:AreaC(1,1,100,100)
robots
  robot robot1
  comenzar
    Pos(1,17)
    derecha
    repetir 49
      Pos(PosAv+2,17)
      si HayPapelEnLaBolsa
        depositarPapel
  fin
variables
  R-Info: robot1
comenzar
  AsignarArea(R-Info,ciudad)
  Iniciar(R-Info,1,1)
fin
```

Código completo: [`../codigo/ejercicio-09.ri`](../codigo/ejercicio-09.ri)

## Corrección aplicada durante esta organización

El archivo histórico usaba `HayFlorEnLaBolsa`/`depositarFlor` en vez de `HayPapelEnLaBolsa`/`depositarPapel`, igual que el ejercicio 2 — el enunciado y el comentario `{...}` del archivo hablan de papeles. Se corrigió el tipo de objeto sin tocar la lógica de movimiento (los saltos con `Pos` no dependen del giro `derecha` inicial, que en este archivo no afecta el resultado porque el reposicionamiento es siempre absoluto).

## Escenario de prueba

Conviene iniciar la simulación con algunos papeles en la bolsa del robot para ver el depósito en las avenidas 3, 5, 7… hasta 99.

## Casos límite

- La esquina de partida (1,17) —avenida impar— nunca recibe depósito, porque el primer `Pos` del `repetir` ya la salta a la avenida 3.
- El recorrido llega hasta la avenida 99 (última impar antes de 100) con las 49 repeticiones (1 + 2×49 = 99); el enunciado describe el final como "la esquina (100,17)", pero el código nunca visita literalmente la avenida 100 (par, fuera del patrón de avenidas impares) — vale la pena tenerlo presente al leer el enunciado junto al código, no se modificó el límite de la repetición porque no es un error de una palabra sino una cuestión de interpretación del punto de corte.

## Errores frecuentes

- Confundir flor y papel al escribir la condición/la primitiva (el bug real que tenía este archivo antes de esta organización).
- Calcular mal la cantidad de repeticiones necesarias para cubrir todas las avenidas impares entre 1 y 99.

## Complejidad

49 saltos fijos: O(1) respecto al tamaño de la ciudad (el rango de avenidas está fijo en el código).

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-09-depositar-papel-avenidas-impares.md`](../ejercicios/ejercicio-09-depositar-papel-avenidas-impares.md)
- Fuente original: [`../fuentes/Capitulo 2-Algoritmos y Logica.pdf`](<../fuentes/Capitulo 2-Algoritmos y Logica.pdf>)
- Código: [`../codigo/ejercicio-09.ri`](../codigo/ejercicio-09.ri)
