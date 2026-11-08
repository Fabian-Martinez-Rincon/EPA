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
  - av: 1
    ca: 1
    flores: 1
escenario_bolsa:
  flores: 10
  papeles: 10
---

# Solución: reforzar en el perímetro las esquinas de un solo tipo

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-05-perimetro-reforzar-esquinas-un-tipo.md`](../ejercicios/ejercicio-05-perimetro-reforzar-esquinas-un-tipo.md).

## Análisis

El enunciado pide reforzar (agregar un objeto más del mismo tipo) en las esquinas que ya tienen sólo flor o sólo papel — no vaciarlas ni cambiarlas de tipo. El código recorre los 4 lados del perímetro con el patrón conocido (`repetir 99 {chequeo+depósito; mover}` + `derecha`), y en cada esquina evalúa `HayFlorEnLaEsquina & ~HayPapelEnLaEsquina` (sólo flor) para depositar una flor más, o el caso simétrico para papel. El chequeo ocurre siempre **antes** de moverse, así que el primer chequeo de cada lado ya cubre el vértice donde terminó el lado anterior — no hace falta (y, como se explica abajo, no hay que agregar) un chequeo extra después de girar.

## Estrategia

1. Repetir 4 veces (una por lado): recorrer 99 esquinas depositando una flor en las que sólo tienen flor y un papel en las que sólo tienen papel, contando cada refuerzo; girar a la derecha para encarar el lado siguiente (el primer chequeo de ese lado, antes de moverse, procesa el vértice donde se giró).
2. Informar los dos contadores.

## Código relacionado

```rinfo
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

## Corrección aplicada durante esta organización

El archivo histórico tenía, después de cada `derecha`, un chequeo/depósito extra para "procesar el vértice":

```
      derecha
      si((HayFlorEnLaEsquina)&~(HayPapelEnLaEsquina))
        flores:=flores+1
        depositarFlor
      si((HayPapelEnLaEsquina)&~(HayFlorEnLaEsquina))
        papeles:=papeles+1
        depositarPapel
```

Ese chequeo es redundante: como el patrón interno ya chequea la esquina actual *antes* de moverse, el primer chequeo del lado siguiente vuelve a caer exactamente sobre el mismo vértice recién procesado. El resultado es que los 4 vértices del perímetro — (1,100), (100,100), (100,1) y el punto de partida (1,1), que se vuelve a chequear al cerrar el recorrido — quedaban **contados y reforzados dos veces** en vez de una. Verificado con el intérprete de R-info: con las cuatro esquinas del perímetro cargadas con "sólo papel" ((1,1), (1,100), (100,100), (100,1), 5 papeles cada una) y bolsa con 20 flores y 20 papeles, la versión histórica llamaba a `depositarPapel` 8 veces (dos por vértice) e informaba `papeles=8` en lugar de 4; con una esquina intermedia sin vértices, (1,30), el bug no se manifestaba, por eso la revisión previa de esta unidad no lo había detectado (el escenario de prueba original tampoco usaba vértices).

La corrección fue eliminar el bloque de chequeo/depósito posterior a `derecha`, dejando que el patrón "chequear antes de mover" del `repetir 99` cubra cada vértice una única vez, como primer paso del lado siguiente (y el vértice de partida (1,1) queda cubierto por el primer chequeo del programa, antes del primer `mover`). Se probó la versión corregida contra el intérprete con tres escenarios antes de aplicarla:

1. Las cuatro esquinas del perímetro con "sólo papel": ahora `depositarPapel` se llama exactamente 4 veces e informa `papeles=4` (antes: 8 veces / `papeles=8`).
2. El escenario original del front matter (esquinas no-vértice en (1,30) y (60,100)): sigue informando `(flores=1, papeles=1)`, sin cambios — la corrección no afecta esquinas fuera de los vértices.
3. Un escenario mixto con vértices y no-vértices combinados —incluyendo una esquina fuera del perímetro que no debe tocarse— dio el conteo exacto esperado en cada caso, sin depósitos duplicados ni esquinas de más procesadas.

El escenario de prueba de este visor (front matter) se amplió agregando el vértice (1,1) con una flor para que el caso límite quede cubierto también al abrir la página, no sólo en las pruebas manuales.

## Escenario de prueba

Arrancá con flores y papeles en la bolsa. Si la bolsa está vacía, el programa corta en la primera esquina que tenga que reforzar, con el error `"depositarPapel" sin papeles en la bolsa`.

Probá con 10 de cada uno y la ciudad así: 1 papel en (1,30), 1 flor en (60,100) y 1 flor en (1,1). El robot informa `2` flores y `1` papel. La esquina (1,1) es un vértice y se refuerza una sola vez.

## Casos límite

- El robot pasa por las 396 esquinas del perímetro: cuatro lados de 99 esquinas cada uno.
- Los cuatro vértices son (1,1), (1,100), (100,100) y (100,1). Cada uno se revisa una sola vez.
- Una esquina con flor y papel a la vez, o vacía, no se refuerza.

## Errores frecuentes

- Agregar un chequeo y un depósito extra después de cada `derecha`, para no perderse el vértice. El chequeo va antes del `mover`, así que el vértice ya lo revisa el primer paso del lado siguiente. Con el extra lo reforzás dos veces: cargá los cuatro vértices con sólo papel y el programa informa `8` en lugar de `4`.
- Leer el enunciado como "sacarle la flor o el papel a las esquinas de un solo tipo". Pide lo contrario: dejar uno más del mismo tipo.

## Complejidad

Perímetro fijo de 4×99 esquinas: O(1) respecto al tamaño de la ciudad (perímetro fijo en 100×100).

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-05-perimetro-reforzar-esquinas-un-tipo.md`](../ejercicios/ejercicio-05-perimetro-reforzar-esquinas-un-tipo.md)
- Código: [`../codigo/soluciones/capitulo-04/Capitulo 4 pregunta 5`](<../codigo/soluciones/capitulo-04/Capitulo 4 pregunta 5>)
