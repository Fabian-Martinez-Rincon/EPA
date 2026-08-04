---
id: "EPA-U04-EJ04-SOLUCION"
titulo: "Solución: contar las esquinas de la calle 20 que tienen sólo papeles"
slug: "ejercicio-04-esquinas-solo-papeles-calle-20"
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
  - "../ejercicios/ejercicio-04-esquinas-solo-papeles-calle-20.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-04/Capitulo 4 pregunta 4"
escenario_ciudad:
  - av: 5
    ca: 20
    papeles: 2
  - av: 8
    ca: 20
    flores: 1
  - av: 10
    ca: 20
    flores: 1
    papeles: 1
---

# Solución: contar las esquinas de la calle 20 que tienen sólo papeles

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-04-esquinas-solo-papeles-calle-20.md`](../ejercicios/ejercicio-04-esquinas-solo-papeles-calle-20.md).

## Análisis

Como no se puede modificar el contenido de las esquinas, la única forma de "contar" es preguntar con las funciones booleanas `HayFlorEnLaEsquina`/`HayPapelEnLaEsquina` sin usar `tomarFlor`/`tomarPapel`. Una esquina es "sólo papel" cuando hay papel y no hay flor: `HayPapelEnLaEsquina & ~HayFlorEnLaEsquina`. El recorrido usa el patrón estándar `repetir 99 {chequeo; mover} + chequeo final` para cubrir las 100 esquinas de la calle 20.

## Estrategia

1. Posicionar el robot en (1,20) y girar a la derecha para recorrer la calle.
2. Repetir 99 veces: si la esquina tiene papel y no tiene flor, contarla; si tiene flor y no papel, contarla aparte; avanzar.
3. Repetir el mismo chequeo (sin avanzar) para la esquina final.
4. Informar ambos contadores.

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
    Pos(1,20)
    derecha
    repetir 99
      si ((HayFlorEnLaEsquina)& ~(HayPapelEnLaEsquina))
        flores:=flores+1
      si ((HayPapelEnLaEsquina)&~(HayFlorEnLaEsquina))
        papeles:=papeles+1
      mover
    si((HayFlorEnLaEsquina)&~(HayPapelEnLaEsquina))
      flores:=flores+1
    si((HayPapelEnLaEsquina)&~(HayFlorEnLaEsquina))
      papeles:=papeles+1
    Informar(flores,papeles)
  fin
variables
  robin:robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-04/Capitulo 4 pregunta 4`](<../codigo/soluciones/capitulo-04/Capitulo 4 pregunta 4>)

## Nota de alcance: informa un dato de más

El enunciado sólo pide la cantidad de esquinas con sólo papeles; el código además calcula e informa la cantidad de esquinas con sólo flores (`flores`). Ese dato extra no contradice lo pedido —el número de "sólo papeles" sigue estando ahí y es correcto— así que no se lo considera un error, sólo información adicional no solicitada. No se quitó del código para no alterar la estructura de la solución histórica.

## Escenario de prueba

Cargar en la calle 20 una esquina con sólo papel (por ejemplo, 2 papeles en avenida 5), una con sólo flor (1 flor en avenida 8) y una mixta (1 flor y 1 papel en avenida 10). Probado con el intérprete: informa `(flores=1, papeles=1)` — la esquina mixta no cuenta para ninguno de los dos contadores, como corresponde.

## Casos límite

- Esquina con flor y papel a la vez: no cuenta ni como "sólo flor" ni como "sólo papel".
- Esquina vacía: tampoco cuenta para ninguno de los dos.

## Errores frecuentes

- Usar `tomarFlor`/`tomarPapel` para "revisar" el contenido de la esquina, lo que violaría la restricción de no modificar nada.
- Escribir la condición de "sólo X" sin negar la presencia del otro tipo, contando también las esquinas mixtas.

## Complejidad

Recorrido fijo de 100 esquinas (una calle completa): O(1) respecto al tamaño de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-04-esquinas-solo-papeles-calle-20.md`](../ejercicios/ejercicio-04-esquinas-solo-papeles-calle-20.md)
- Código: [`../codigo/soluciones/capitulo-04/Capitulo 4 pregunta 4`](<../codigo/soluciones/capitulo-04/Capitulo 4 pregunta 4>)
