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
- **Recorrido c) — `Cap5_4C` y `Cap5_4C otro`**: ambos alternan la orientación del rectángulo entre una invocación y la siguiente usando `izquierda`/`derecha` antes y después de la segunda llamada, de modo que el segundo rectángulo de cada par queda rotado 90° respecto del primero (el lado de 3 y el de 5 quedan intercambiados entre avenida y calle) antes de saltar con `Pos` al siguiente par. `Cap5_4C` escribe `rectangulo` de forma compacta (`repetir 2` envolviendo los dos pares lado-giro) mientras que `Cap5_4C otro` lo escribe totalmente desenrollado; ambos son equivalentes lado a lado y usan los mismos saltos relativos de `Pos`, solo que con offsets absolutos distintos (`PosAv+9`/`+1` en un caso, `PosAv+10`/`+2` en el otro) — dos soluciones alternativas al mismo recorrido, no una corrección de la otra.

## Estrategia

1. Reutilizar el proceso `rectangulo` del ejercicio 3, incluido su cuarto giro final (que cierra la orientación igual que al empezar).
2. Para el recorrido a): repetir "rectángulo + `Pos(1,PosCa+5)`" tres veces.
3. Para el recorrido b): repetir "rectángulo + `Pos(PosAv+1,PosCa+1)`" tres veces.
4. Para el recorrido c): alternar la orientación del rectángulo (con `izquierda`/`derecha`) entre invocaciones sucesivas y saltar con `Pos` a lo largo de la avenida.

## Código relacionado

**Recorrido a) — proceso principal:**

```
comenzar
  repetir 3
    rectangulo
    Pos(1,PosCa+5)
fin
```

Código completo: [`../codigo/soluciones/capitulo-05/Cap5_4A`](<../codigo/soluciones/capitulo-05/Cap5_4A>)

**Recorrido b) — proceso principal:**

```
comenzar
  repetir 3
    rectangulo
    Pos(PosAv+1,PosCa+1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-05/Cap5_4B`](<../codigo/soluciones/capitulo-05/Cap5_4B>)

**Recorrido c) — proceso principal:**

```
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

## Consistencia con el ejercicio 3: el rectángulo cierra el giro en toda la familia

Los cuatro archivos de este ejercicio reutilizan el proceso `rectangulo` con su cuarto `derecha` final incluido. Originalmente esto era una diferencia con el archivo histórico del ejercicio 3 (`Cap5_3`), al que le faltaba ese giro; se agregó a `Cap5_3` por consistencia con esta familia (ver la sección "Corrección aplicada" en su solución), así que ahora los cinco archivos (3, 4A, 4B, 4C y "4C otro") comparten exactamente el mismo proceso `rectangulo` de 4 giros. Esto importa en particular para el recorrido c), que depende de que `rectangulo` termine orientado igual que empezó para que el `izquierda`/`derecha` posterior tenga el efecto esperado sobre la orientación del segundo rectángulo del par.

## Escenario de prueba

Ninguno de los cuatro programas depende del contenido de las esquinas; alcanza con correr cada uno sobre una ciudad vacía y observar la disposición de los rectángulos trazados (columna vertical en a, escalera diagonal superpuesta en b, fila horizontal alternando orientación en c).

## Casos límite

- Todos los saltos entre rectángulos usan `Pos` (absoluto), no `mover`, por lo que la orientación previa nunca afecta dónde se ubica el siguiente rectángulo — solo afecta, en el caso de c), la forma en que se traza ese siguiente rectángulo (girado o no).
- Con las repeticiones tal como están en los cuatro archivos (`repetir 3` en a y b, `repetir 2` de pares en c), todos los recorridos caben dentro de `AreaC(1,1,100,100)` partiendo de (1,1).

## Errores frecuentes

- Reimplementar el rectángulo dentro del proceso que arma el recorrido en vez de reutilizar el proceso `rectangulo` del ejercicio 3 — contradice el propósito del ejercicio (reuso de módulos).
- En el recorrido c), olvidar el giro de orientación (`izquierda`/`derecha`) entre el primer y el segundo rectángulo de cada par, lo que haría que ambos queden con la misma orientación (5 de base) en vez de intercalar orientaciones (5 y 3 de base alternados) como muestra la figura.

## Complejidad

Cada recorrido traza una cantidad fija de rectángulos (3 en a y b, 4 en c): O(1) respecto al tamaño de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-04-recorridos-con-rectangulo.md`](../ejercicios/ejercicio-04-recorridos-con-rectangulo.md)
- Fuente original: [`../fuentes/Capitulo 5-Programacion Estructurada.pdf`](<../fuentes/Capitulo 5-Programacion Estructurada.pdf>)
- Figura: [`../recursos/figura-5-10-recorridos-rectangulos.png`](<../recursos/figura-5-10-recorridos-rectangulos.png>)
- Código: [`../codigo/soluciones/capitulo-05/Cap5_4A`](<../codigo/soluciones/capitulo-05/Cap5_4A>), [`../codigo/soluciones/capitulo-05/Cap5_4B`](<../codigo/soluciones/capitulo-05/Cap5_4B>), [`../codigo/soluciones/capitulo-05/Cap5_4C`](<../codigo/soluciones/capitulo-05/Cap5_4C>), [`../codigo/soluciones/capitulo-05/Cap5_4C otro`](<../codigo/soluciones/capitulo-05/Cap5_4C otro>)
- Prerrequisito: [ejercicio 3](ejercicio-03-rectangulo-5x3-horario.md)
