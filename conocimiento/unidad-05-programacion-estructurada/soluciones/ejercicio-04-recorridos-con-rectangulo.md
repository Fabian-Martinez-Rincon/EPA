---
id: "EPA-U05-EJ04-SOLUCION"
titulo: "Solución: recorridos de la figura 5.10 usando el proceso rectángulo"
slug: "ejercicio-04-recorridos-con-rectangulo"
tipo: "solucion"
unidad: 5
tema: "programacion-estructurada"
subtemas:
  - "programacion-modular"
  - "reusabilidad-de-procesos"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 5-Programacion Estructurada.pdf"
    paginas: "1-24"
relacionados:
  - "../ejercicios/ejercicio-04-recorridos-con-rectangulo.md"
  - "../soluciones/ejercicio-03-rectangulo-5x3-horario.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-05/Cap5_4A"
  - "../codigo/soluciones/capitulo-05/Cap5_4B"
  - "../codigo/soluciones/capitulo-05/Cap5_4C"
  - "../codigo/soluciones/capitulo-05/Cap5_4C otro"
---

# Solución: recorridos de la figura 5.10 usando el proceso rectángulo

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-04-recorridos-con-rectangulo.md`](../ejercicios/ejercicio-04-recorridos-con-rectangulo.md).

## Análisis

Los cuatro archivos reutilizan el proceso `rectangulo` del ejercicio 3 (con el cuarto giro agregado — ver más abajo) y solo cambian cómo se reposiciona el robot entre una invocación y la siguiente, usando siempre `Pos` (coordenadas absolutas):

- **Recorrido a) — `Cap5_4A`**: `repetir 3: rectangulo; Pos(1,PosCa+5)`. Como cada `rectangulo` vuelve a la esquina donde fue invocado, esto apila tres rectángulos uno sobre otro a lo largo del eje de la calle, siempre en la avenida 1 — la columna vertical que pide el recorrido a).
- **Recorrido b) — `Cap5_4B`**: `repetir 3: rectangulo; Pos(PosAv+1,PosCa+1)`. El paso diagonal de solo 1 esquina hace que los rectángulos de 5x3 sucesivos queden fuertemente superpuestos entre sí, formando la figura escalonada compacta del recorrido b).
- **Recorrido c) — `Cap5_4C` y `Cap5_4C otro`**: ambos alternan la orientación del rectángulo entre una invocación y la siguiente usando `izquierda`/`derecha` antes y después de la segunda llamada, de modo que el segundo rectángulo de cada par queda rotado 90° respecto del primero (el lado de 3 y el de 5 quedan intercambiados entre avenida y calle) antes de saltar con `Pos` al siguiente par. `Cap5_4C` escribe `rectangulo` de forma compacta (`repetir 2` envolviendo los dos pares lado-giro) mientras que `Cap5_4C otro` lo escribe totalmente desenrollado. No dibujan la misma figura: con los saltos de `Cap5_4C` (`PosAv+9`/`+1`) el recorrido cubre las avenidas 1 a 21 sin dejar ninguna vacía, y con los de `Cap5_4C otro` (`PosAv+10`/`+2`) llega hasta la avenida 25 dejando vacías la 7, la 12, la 19 y la 24. El enunciado pide los cuatro rectángulos "uno junto a otro", así que el fiel es `Cap5_4C`.

## Estrategia

1. Reutilizar el proceso `rectangulo` del ejercicio 3, incluido su cuarto giro final (que cierra la orientación igual que al empezar).
2. Para el recorrido a): repetir "rectángulo + `Pos(1,PosCa+5)`" tres veces.
3. Para el recorrido b): repetir "rectángulo + `Pos(PosAv+1,PosCa+1)`" tres veces.
4. Para el recorrido c): alternar la orientación del rectángulo (con `izquierda`/`derecha`) entre invocaciones sucesivas y saltar con `Pos` a lo largo de la avenida.

## Código relacionado

**Recorrido a) — proceso principal:**

```rinfo
comenzar
  repetir 3
    rectangulo
    Pos(1,PosCa+5)
fin
```

Código completo: [`../codigo/soluciones/capitulo-05/Cap5_4A`](<../codigo/soluciones/capitulo-05/Cap5_4A>)

**Recorrido b) — proceso principal:**

```rinfo
comenzar
  repetir 3
    rectangulo
    Pos(PosAv+1,PosCa+1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-05/Cap5_4B`](<../codigo/soluciones/capitulo-05/Cap5_4B>)

**Recorrido c) — proceso principal:**

```rinfo
comenzar
  repetir 2
    rectangulo
    izquierda
    Pos(PosAv+9,1)
    rectangulo
    derecha
    Pos(PosAv+1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-05/Cap5_4C`](<../codigo/soluciones/capitulo-05/Cap5_4C>) y variante alternativa en [`../codigo/soluciones/capitulo-05/Cap5_4C otro`](<../codigo/soluciones/capitulo-05/Cap5_4C otro>)

## Corrección aplicada durante esta organización (consistencia, sin efecto de comportamiento)

Los cuatro archivos conservan, sin usar, una copia completa de los procesos `cuadrado`, `A` y `B` de los ejercicios 1 y 2 (heredada de copiar el mismo bloque de `procesos` de archivo en archivo). El `cuadrado` de esas copias tenía el mismo `repetir 3` incorrecto descripto en la solución del ejercicio 1; se corrigió a `repetir 2` en los cuatro archivos por consistencia con el resto del capítulo, aunque al ser código muerto (nunca invocado desde estos programas) no cambia el comportamiento de ninguno de los cuatro — se verificó con el intérprete que la cantidad de eventos generados es idéntica antes y después del cambio.

## Por qué el rectángulo cierra con un cuarto giro

Los cuatro programas usan un `rectangulo` que cierra con un cuarto `derecha`, igual que el del ejercicio 3. El de `Cap5_4C` está escrito más corto, con un `repetir 2` que envuelve los dos pares de lado y giro, pero hace exactamente lo mismo.

Ese cuarto giro es el que hace andar el recorrido c). Si `rectangulo` no devolviera al robot a la orientación de arranque, el `izquierda` y el `derecha` que vienen después no rotarían el rectángulo siguiente.

## Escenario de prueba

Ciudad vacía en los cuatro programas. Lo que se mira es dónde cae cada rectángulo.

- **a)** tres rectángulos apilados en la avenida 1, arrancando en las calles 1, 6 y 11.
- **b)** tres rectángulos que arrancan en (1,1), (2,2) y (3,3), muy montados uno sobre otro.
- **c)** cuatro rectángulos en fila sobre la calle 1, alternando orientación: el primero de 5 de ancho, el segundo de 3, y así.

## Casos límite

- Los cuatro saltan con `Pos`, nunca con `mover`. La orientación previa no decide dónde cae el rectángulo siguiente. En c) sí decide cómo se dibuja, porque ahí el `izquierda` lo rota 90 grados.
- Los dos programas de c) no dibujan lo mismo. `Cap5_4C` deja los cuatro rectángulos pegados: avenidas 1 a 6, 7 a 10, 11 a 16 y 17 a 20. `Cap5_4C otro` salta de a `+10` y `+2` en vez de `+9` y `+1`, y deja una avenida vacía entre uno y otro: 1 a 6, 8 a 11, 13 a 18 y 20 a 23. La figura del enunciado los muestra pegados.
- Todo entra cómodo en la ciudad. El que más lejos llega es `Cap5_4C otro`, hasta la avenida 23.

## Errores frecuentes

- Copiar el cuerpo del rectángulo adentro del programa en vez de invocar `rectangulo`. El ejercicio pide reusar el proceso del ejercicio 3.
- En c), olvidarse del `izquierda` antes del segundo rectángulo del par. Los cuatro salen con la base de 5 sobre la avenida y la fila deja de alternar.

## Complejidad

Cada recorrido traza una cantidad fija de rectángulos (3 en a y b, 4 en c): O(1) respecto al tamaño de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-04-recorridos-con-rectangulo.md`](../ejercicios/ejercicio-04-recorridos-con-rectangulo.md)
- Figura: [`../recursos/figura-5-10-recorridos-rectangulos.png`](<../recursos/figura-5-10-recorridos-rectangulos.png>)
- Código: [`../codigo/soluciones/capitulo-05/Cap5_4A`](<../codigo/soluciones/capitulo-05/Cap5_4A>), [`../codigo/soluciones/capitulo-05/Cap5_4B`](<../codigo/soluciones/capitulo-05/Cap5_4B>), [`../codigo/soluciones/capitulo-05/Cap5_4C`](<../codigo/soluciones/capitulo-05/Cap5_4C>), [`../codigo/soluciones/capitulo-05/Cap5_4C otro`](<../codigo/soluciones/capitulo-05/Cap5_4C otro>)
- Prerrequisito: [ejercicio 3](ejercicio-03-rectangulo-5x3-horario.md)
