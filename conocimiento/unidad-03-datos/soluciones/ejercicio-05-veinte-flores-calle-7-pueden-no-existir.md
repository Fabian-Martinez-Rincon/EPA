---
id: "EPA-U03-EJ05-SOLUCION"
titulo: "Solución: caminar la calle 7 hasta encontrar 20 flores (pueden no existir)"
slug: "ejercicio-05-veinte-flores-calle-7-pueden-no-existir"
tipo: "solucion"
unidad: 3
tema: "datos-y-variables"
subtemas:
  - "variables"
  - "estructuras-de-control"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "parcial"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 3-Datos.pdf"
    paginas: "1-21"
relacionados:
  - "../ejercicios/ejercicio-05-veinte-flores-calle-7-pueden-no-existir.md"
  - "../soluciones/ejercicio-04-veinte-flores-calle-7-garantizadas.md"
codigo_relacionado:
  - "../codigo/capitulo-3-pregunta-05.ri"
escenario_ciudad:
  - av: 5
    ca: 7
    flores: 1
  - av: 10
    ca: 7
    flores: 1
  - av: 15
    ca: 7
    flores: 1
  - av: 20
    ca: 7
    flores: 1
  - av: 25
    ca: 7
    flores: 1
  - av: 30
    ca: 7
    flores: 1
  - av: 35
    ca: 7
    flores: 1
  - av: 40
    ca: 7
    flores: 1
---

# Solución: caminar la calle 7 hasta encontrar 20 flores (pueden no existir)

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-05-veinte-flores-calle-7-pueden-no-existir.md`](../ejercicios/ejercicio-05-veinte-flores-calle-7-pueden-no-existir.md).

## Análisis

A diferencia del ejercicio 4, acá no se garantiza que existan 20 flores, así que el corte del recorrido no puede depender sólo de `x<20`: hace falta combinarlo con el límite de la calle (`PosAv<100`). El robot avanza mientras no se acabó la calle; en cada esquina, sólo si todavía no llegó a 20 flores intenta tomar una.

## Estrategia

1. Posicionar el robot en (1,7) y girar a la derecha.
2. Mientras `PosAv<100`: si `x<20` y hay flor en la esquina, tomarla y contarla; avanzar (siempre, haya o no encontrado flor).
3. Informar `x`.

## Código relacionado

```
programa prueba
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  variables
    x: numero
    y: numero
  comenzar
    Pos(1,7)
    x:=0
    derecha
    mientras(PosAv<100)
      si(x<20)
        si(HayFlorEnLaEsquina)
          tomarFlor
          x:=x+1
      mover
    Informar(x)
  fin
variables
  robin:robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/capitulo-3-pregunta-05.ri`](../codigo/capitulo-3-pregunta-05.ri)

## Corrección aplicada durante esta organización

En el archivo histórico, `mover` estaba anidado **dentro** del `si(x<20)`, en vez de ser una instrucción del cuerpo del `mientras(PosAv<100)` que se ejecuta siempre. El efecto: en cuanto `x` llegaba a 20 antes de que `PosAv` llegara a 100, `mover` dejaba de ejecutarse (porque `x<20` ya era falso), con lo cual `PosAv` quedaba congelado y el `mientras(PosAv<100)` exterior nunca terminaba — un loop infinito. Se verificó con el intérprete de R-info: cargando 20 flores en las avenidas 1 a 20 de la calle 7, el archivo original se cuelga (supera el límite de pasos del intérprete, señal de loop infinito); con `mover` desanidado (al mismo nivel que `si(x<20)`, ejecutándose en cada vuelta del `mientras` exterior) el programa informa correctamente `x=20` y termina. También se probó sin flores (informa `x=0`) y con sólo 8 flores disponibles (informa `x=8`); en los tres casos el programa corregido termina normalmente.

## Alcance no corregido: la avenida 100 no se chequea

Tal como queda el archivo (antes y después de la corrección de arriba), el `mientras(PosAv<100)` deja de procesar esquinas apenas `PosAv` llega a 100 — la esquina (100,7) nunca se chequea. Si la flor número 20 (o alguna de las últimas necesarias) estuviera justo ahí, el programa terminaría informando un valor menor a 20 aun cuando sí hubiera 20 flores en la calle. Arreglar esto implicaría agregar un bloque nuevo después del `mientras` para procesar esa última esquina (como hace el ejemplo 3.7 de la teoría) — se documenta la limitación en vez de agregarlo, en la misma línea que la nota sobre la avenida 100 en `ejercicio-09` de la unidad 2.

## Escenario de prueba

Cargar menos de 20 flores en la calle 7 (por ejemplo, 8, en avenidas dispersas) para observar que el robot recorre toda la calle y termina informando la cantidad real encontrada, sin colgarse. También se puede cargar exactamente 20 para confirmar que corta apenas las junta.

## Casos límite

- Sin flores en la calle: `x` termina en 0.
- Menos de 20 flores: `x` informa la cantidad real encontrada al llegar al final de la calle.
- 20 flores, la última en la avenida 100: no se contaría (ver nota de alcance).

## Errores frecuentes

- Anidar una instrucción de avance dentro de una condición que puede volverse falsa antes de cumplirse la condición de corte del bucle exterior — el bug real que tenía este archivo, y una fuente común de loops infinitos en este lenguaje (no hay `break`, así que todo el control de corte depende de las condiciones de los `mientras`).

## Complejidad

Recorrido de hasta 100 esquinas (una calle completa): O(1) respecto al tamaño de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-05-veinte-flores-calle-7-pueden-no-existir.md`](../ejercicios/ejercicio-05-veinte-flores-calle-7-pueden-no-existir.md)
- Fuente original: [`../fuentes/Capitulo 3-Datos.pdf`](<../fuentes/Capitulo 3-Datos.pdf>)
- Código: [`../codigo/capitulo-3-pregunta-05.ri`](../codigo/capitulo-3-pregunta-05.ri)
