---
id: "EPA-U05-EJ03-SOLUCION"
titulo: "Solución: proceso rectángulo de base 5 y altura 3 en sentido horario"
slug: "ejercicio-03-rectangulo-5x3-horario"
tipo: "solucion"
unidad: 5
tema: "programacion-estructurada"
subtemas:
  - "programacion-modular"
  - "procesos-sin-parametros"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 5-Programacion Estructurada.pdf"
    paginas: "1-24"
relacionados:
  - "../ejercicios/ejercicio-03-rectangulo-5x3-horario.md"
  - "../soluciones/ejercicio-04-recorridos-con-rectangulo.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-05/Cap5_3"
---

# Solución: proceso rectángulo de base 5 y altura 3 en sentido horario

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-03-rectangulo-5x3-horario.md`](../ejercicios/ejercicio-03-rectangulo-5x3-horario.md).

## Análisis

Un rectángulo tiene 4 lados, mueve el mismo esquema que un cuadrado pero alternando dos longitudes distintas: base (5) y altura (3). Partiendo del robot en (1,1) con su orientación por defecto (`mover` sin girar incrementa `PosCa`, es decir el robot arranca "mirando" a lo largo de una calle), el código traza: 3 esquinas (altura), giro horario, 5 esquinas (base), giro horario, 3 esquinas (altura), giro horario, 5 esquinas (base). Esto recorre el perímetro completo de un rectángulo de 5x3 y el robot vuelve a quedar exactamente en (1,1) (la posición no depende del último giro, solo los avances la determinan).

## Estrategia

1. Avanzar 3 esquinas, girar a la derecha.
2. Avanzar 5 esquinas, girar a la derecha.
3. Avanzar 3 esquinas, girar a la derecha.
4. Avanzar 5 esquinas.

## Código relacionado

```
proceso rectangulo
comenzar
  repetir 3
    mover
  derecha
  repetir 5
    mover
  derecha
  repetir 3
    mover
  derecha
  repetir 5
    mover
fin
```

Código completo: [`../codigo/soluciones/capitulo-05/Cap5_3`](<../codigo/soluciones/capitulo-05/Cap5_3>)

## Nota de fidelidad: falta el giro final

El enunciado no pide explícitamente que el robot quede orientado de determinada manera al terminar, y en efecto el código deja al robot exactamente en (1,1) (la esquina de partida) sin importar el giro final, porque los giros no mueven al robot, solo lo reorientan. Sin embargo, comparado con los procesos `cuadrado` de los ejercicios 1 y 2 —que sí cierran el giro y devuelven al robot a la **misma orientación** de inicio, propiedad explicada en el Ejemplo 5.6 de la teoría— a este `rectangulo` le falta el cuarto `derecha` después del último `repetir 5: mover`. Esto se confirma comparando contra los cuatro archivos del ejercicio 4 (`Cap5_4A`, `Cap5_4B`, `Cap5_4C`, `Cap5_4C otro`), que reutilizan literalmente este mismo proceso `rectangulo` pero **sí** incluyen el cuarto giro.

No se agregó el giro faltante en este archivo porque, a diferencia del bug de `cuadrado` en los ejercicios 1 y 2 (una sustitución de un número por otro, con evidencia textual directa de cuál era el valor correcto), acá se trataría de **agregar una instrucción completa que no está** — un cambio de una categoría distinta (más cercano a "falta lógica" que a "un operador equivocado"), y el enunciado de este ejercicio en particular no exige ese comportamiento. Se documenta la discrepancia en vez de "adivinar y corregir"; quien reutilice este proceso para encadenar varios rectángulos con `mover` (en lugar de con `Pos`, que no depende de la orientación) debe tener en cuenta que el robot no queda orientado igual que al empezar.

## Escenario de prueba

El proceso no depende del contenido de las esquinas; alcanza con correr el programa sobre una ciudad vacía y observar que el robot recorre un rectángulo de 5 (base, a lo largo de la avenida) por 3 (altura, a lo largo de la calle) y vuelve a (1,1).

## Casos límite

- El robot vuelve exactamente a la esquina de partida (1,1), pero **no** a la misma orientación con la que empezó (ver nota de fidelidad arriba) — importa si este proceso se reutiliza seguido de un `mover` en vez de un `Pos`.
- Si se invocara este proceso desde una esquina cercana al borde del área, el rectángulo podría salirse de la ciudad; desde (1,1) con `AreaC(1,1,100,100)` no hay riesgo.

## Errores frecuentes

- Confundir cuál de las dos longitudes (5 o 3) corresponde a la "base" y cuál a la "altura": acá la base (5) queda a lo largo de la avenida y la altura (3) a lo largo de la calle, dado el punto de partida y la orientación inicial del robot.
- Asumir que el proceso deja al robot orientado igual que al empezar, como sí ocurre con el `cuadrado` de los ejercicios 1 y 2 (ver nota de fidelidad).

## Complejidad

Un recorrido fijo de 16 movimientos y 3 giros por invocación: O(1) respecto al tamaño de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-03-rectangulo-5x3-horario.md`](../ejercicios/ejercicio-03-rectangulo-5x3-horario.md)
- Fuente original: [`../fuentes/Capitulo 5-Programacion Estructurada.pdf`](<../fuentes/Capitulo 5-Programacion Estructurada.pdf>)
- Código: [`../codigo/soluciones/capitulo-05/Cap5_3`](<../codigo/soluciones/capitulo-05/Cap5_3>)
- Comparar con: [`../codigo/soluciones/capitulo-05/Cap5_4A`](<../codigo/soluciones/capitulo-05/Cap5_4A>), que reutiliza este proceso con el cuarto giro agregado.
