---
id: "EPA-U04-EJ05-SOLUCION"
titulo: "Solución: reforzar en el perímetro las esquinas de un solo tipo"
slug: "ejercicio-05-perimetro-reforzar-esquinas-un-tipo"
tipo: "solucion"
unidad: 4
tema: "repaso-integrador"
subtemas:
  - "repaso-de-variables"
  - "repaso-de-expresiones-logicas"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 4-Repaso.pdf"
    paginas: "1-12"
relacionados:
  - "../ejercicios/ejercicio-05-perimetro-reforzar-esquinas-un-tipo.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-04/Capitulo 4 pregunta 5"
escenario_ciudad:
  - av: 1
    ca: 30
    papeles: 1
  - av: 60
    ca: 100
    flores: 1
escenario_bolsa:
  flores: 10
  papeles: 10
---

# Solución: reforzar en el perímetro las esquinas de un solo tipo

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-05-perimetro-reforzar-esquinas-un-tipo.md`](../ejercicios/ejercicio-05-perimetro-reforzar-esquinas-un-tipo.md).

## Análisis

El enunciado pide reforzar (agregar un objeto más del mismo tipo) en las esquinas que ya tienen sólo flor o sólo papel — no vaciarlas ni cambiarlas de tipo. El código recorre los 4 lados del perímetro con el patrón conocido (`repetir 99 {chequeo+depósito; mover}` + chequeo del vértice + `derecha`), y en cada esquina evalúa `HayFlorEnLaEsquina & ~HayPapelEnLaEsquina` (sólo flor) para depositar una flor más, o el caso simétrico para papel.

## Estrategia

1. Repetir 4 veces (una por lado): recorrer 99 esquinas depositando una flor en las que sólo tienen flor y un papel en las que sólo tienen papel, contando cada refuerzo; girar a la derecha; procesar el vértice de la misma manera.
2. Informar los dos contadores.

## Código relacionado

```
programa prueba
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  variables
    flores: numero
    papeles: numero
  comenzar
    flores:=0
    papeles:=0
    repetir 4
      repetir 99
        si ((HayFlorEnLaEsquina)& ~(HayPapelEnLaEsquina))
          flores:=flores+1
          depositarFlor
        si ((HayPapelEnLaEsquina)&~(HayFlorEnLaEsquina))
          papeles:=papeles+1
          depositarPapel
        mover
      derecha
      si((HayFlorEnLaEsquina)&~(HayPapelEnLaEsquina))
        flores:=flores+1
        depositarFlor
      si((HayPapelEnLaEsquina)&~(HayFlorEnLaEsquina))
        papeles:=papeles+1
        depositarPapel
    Informar(flores,papeles)
  fin
variables
  robin:robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-04/Capitulo 4 pregunta 5`](<../codigo/soluciones/capitulo-04/Capitulo 4 pregunta 5>)

## Escenario de prueba

Este ejercicio necesita que la bolsa del robot arranque con al menos una flor y un papel, porque `depositarFlor`/`depositarPapel` fallan si la bolsa está vacía; probado con el intérprete de R-info, con la bolsa vacía el programa corta con el error `"depositarPapel" sin papeles en la bolsa`. Con una bolsa inicial de, por ejemplo, 10 flores y 10 papeles, y con una esquina del perímetro con sólo papel (1 papel en (1,30)) y otra con sólo flor (1 flor en (60,100)), el programa informa correctamente `(flores=1, papeles=1)`.

## Casos límite

- Esquina con flor y papel a la vez, o esquina vacía: no se refuerza en ninguno de los dos casos.
- Bolsa sin flores o sin papeles al llegar a una esquina que los necesita: el depósito falla (ver "Escenario de prueba"); el enunciado no contempla este caso, así que se asume que el robot arranca con provisión suficiente, igual que otros ejercicios de depósito de la unidad 2.

## Errores frecuentes

- Interpretar el enunciado como "vaciar de flor/papel las esquinas de un solo tipo" en vez de "agregar un refuerzo del mismo tipo" — la lectura literal del enunciado (y el código) es la segunda.
- Olvidar que `derecha` gira en el vértice pero no mueve al robot, así que el chequeo del vértice puede hacerse antes o después del giro sin cambiar de esquina.

## Complejidad

Perímetro fijo de 4×99 esquinas: O(1) respecto al tamaño de la ciudad (perímetro fijo en 100×100).

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-05-perimetro-reforzar-esquinas-un-tipo.md`](../ejercicios/ejercicio-05-perimetro-reforzar-esquinas-un-tipo.md)
- Fuente original: [`../fuentes/Capitulo 4-Repaso.pdf`](<../fuentes/Capitulo 4-Repaso.pdf>)
- Código: [`../codigo/soluciones/capitulo-04/Capitulo 4 pregunta 5`](<../codigo/soluciones/capitulo-04/Capitulo 4 pregunta 5>)
