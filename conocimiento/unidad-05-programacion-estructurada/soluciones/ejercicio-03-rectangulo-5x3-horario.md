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

Un rectángulo tiene 4 lados, mueve el mismo esquema que un cuadrado pero alternando dos longitudes distintas: base (5) y altura (3). Partiendo del robot en (1,1) con su orientación por defecto (`mover` sin girar incrementa `PosCa`, es decir el robot arranca "mirando" a lo largo de una calle), el código traza: 3 esquinas (altura), giro horario, 5 esquinas (base), giro horario, 3 esquinas (altura), giro horario, 5 esquinas (base), giro horario. Esto recorre el perímetro completo de un rectángulo de 5x3, el robot vuelve a quedar exactamente en (1,1) (la posición no depende de los giros, solo los avances la determinan) y, con el cuarto giro, también queda orientado igual que al empezar — igual que el `cuadrado` de los ejercicios 1 y 2.

## Estrategia

1. Avanzar 3 esquinas, girar a la derecha.
2. Avanzar 5 esquinas, girar a la derecha.
3. Avanzar 3 esquinas, girar a la derecha.
4. Avanzar 5 esquinas, girar a la derecha.

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
  derecha
fin
```

Código completo: [`../codigo/soluciones/capitulo-05/Cap5_3`](<../codigo/soluciones/capitulo-05/Cap5_3>)

## Corrección aplicada: giro final agregado por consistencia

El enunciado de este ejercicio no pide explícitamente que el robot quede orientado de determinada manera al terminar, y el código original ya dejaba al robot exactamente en (1,1) (la esquina de partida) sin importar el giro final, porque los giros no mueven al robot, solo lo reorientan — es decir, el archivo histórico **sí** cumplía lo que su propio enunciado pedía, por eso este ejercicio quedó `"completo"` y no `"parcial"`.

Aun así, el archivo histórico tenía una inconsistencia con el resto de la familia de ejercicios: los procesos `cuadrado` de los ejercicios 1 y 2 sí cierran el giro y devuelven al robot a la **misma orientación** de inicio (propiedad explicada en el Ejemplo 5.6 de la teoría), y las tres variantes reutilizadas del ejercicio 4 (`Cap5_4A`, `Cap5_4B`, `Cap5_4C`, `Cap5_4C otro`) ya incluían un cuarto `derecha` tras el último `repetir 5: mover` que **no** estaba en este archivo original de origen. Se agregó ese cuarto `derecha` al final de `rectangulo` en `Cap5_3` por consistencia con el resto de la familia (1, 2 y las cuatro variantes del 4), no porque el enunciado propio lo exigiera — así el proceso queda uniforme y reutilizable sin sorpresas de orientación en cualquier programa futuro que lo invoque encadenado con `mover`.

Se corrió el archivo actualizado contra el intérprete de R-info (ciudad vacía): el robot traza exactamente el mismo rectángulo de 5 (avenida) x 3 (calle) que antes — recorrido `(1,1)→(1,4)→(6,4)→(6,1)→(1,1)` — y el único cambio observable es que ahora termina con `direccion:0`, igual que al empezar, en vez de `direccion:3`. Ni la posición final ni el trazado del rectángulo cambiaron.

## Escenario de prueba

El proceso no depende del contenido de las esquinas; alcanza con correr el programa sobre una ciudad vacía y observar que el robot recorre un rectángulo de 5 (base, a lo largo de la avenida) por 3 (altura, a lo largo de la calle) y vuelve a (1,1).

## Casos límite

- El robot vuelve exactamente a la esquina de partida (1,1) y, con el giro final agregado, también a la misma orientación con la que empezó — igual que el `cuadrado` de los ejercicios 1 y 2. Esto importa si este proceso se reutiliza encadenado con `mover` en vez de con `Pos` (que no depende de la orientación).
- Si se invocara este proceso desde una esquina cercana al borde del área, el rectángulo podría salirse de la ciudad; desde (1,1) con `AreaC(1,1,100,100)` no hay riesgo.

## Errores frecuentes

- Confundir cuál de las dos longitudes (5 o 3) corresponde a la "base" y cuál a la "altura": acá la base (5) queda a lo largo de la avenida y la altura (3) a lo largo de la calle, dado el punto de partida y la orientación inicial del robot.
- Olvidar el cuarto giro final tras el último tramo — no afecta la posición donde termina el robot (los giros no mueven), pero sí su orientación, lo que importa para cualquier reuso posterior del proceso que dependa de `mover` en vez de `Pos`.

## Complejidad

Un recorrido fijo de 16 movimientos y 4 giros por invocación: O(1) respecto al tamaño de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-03-rectangulo-5x3-horario.md`](../ejercicios/ejercicio-03-rectangulo-5x3-horario.md)
- Fuente original: [`../fuentes/Capitulo 5-Programacion Estructurada.pdf`](<../fuentes/Capitulo 5-Programacion Estructurada.pdf>)
- Código: [`../codigo/soluciones/capitulo-05/Cap5_3`](<../codigo/soluciones/capitulo-05/Cap5_3>)
- Comparar con: [`../codigo/soluciones/capitulo-05/Cap5_4A`](<../codigo/soluciones/capitulo-05/Cap5_4A>), que reutiliza este proceso (ya con el cuarto giro).
