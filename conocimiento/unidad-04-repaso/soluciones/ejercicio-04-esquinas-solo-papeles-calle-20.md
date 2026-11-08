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

## El programa informa dos números, no uno

`Informar(flores,papeles)` muestra primero las esquinas con sólo flor y después las de sólo papel. El enunciado pide el segundo número.

El contador de flores es el mismo chequeo con la condición dada vuelta. Está de más, pero no molesta: el dato que te piden sigue ahí.

## Escenario de prueba

Cargá tres esquinas de la calle 20: 2 papeles en la avenida 5, 1 flor en la avenida 8, y 1 flor más 1 papel en la avenida 10.

El programa informa `1` y `1`. La esquina mixta de la avenida 10 no suma en ningún lado.

## Casos límite

- El `repetir 99` revisa de la avenida 1 a la 99 y deja al robot parado en la 100. Esa última esquina la cubren los dos `si` sueltos de abajo. Si los borrás, la avenida 100 no se cuenta nunca.
- Una esquina vacía no suma a ningún contador. Las dos condiciones piden que haya algo.

## Errores frecuentes

- Usar `tomarPapel` para ver qué hay en la esquina. Tomar el papel la modifica, y el enunciado lo prohíbe. Para mirar sin tocar están `HayPapelEnLaEsquina` y `HayFlorEnLaEsquina`.
- Escribir `si (HayPapelEnLaEsquina)` a secas. Así la avenida 10 del escenario, que tiene flor y papel, también suma. Hace falta el `& ~(HayFlorEnLaEsquina)`.

## Complejidad

Recorrido fijo de 100 esquinas (una calle completa): O(1) respecto al tamaño de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-04-esquinas-solo-papeles-calle-20.md`](../ejercicios/ejercicio-04-esquinas-solo-papeles-calle-20.md)
- Código: [`../codigo/soluciones/capitulo-04/Capitulo 4 pregunta 4`](<../codigo/soluciones/capitulo-04/Capitulo 4 pregunta 4>)
