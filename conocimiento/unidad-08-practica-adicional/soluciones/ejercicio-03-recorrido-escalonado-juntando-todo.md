---
id: "EPA-U08-EJ03-SOLUCION"
titulo: "Solución: recorrido escalonado juntando todas las flores y papeles"
slug: "ejercicio-03-recorrido-escalonado-juntando-todo"
tipo: "solucion"
unidad: 8
tema: "practica-adicional"
subtemas:
  - "modularizacion"
nivel: "intermedio"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Ejercicios Adicionales.pdf"
    paginas: "1-2"
relacionados:
  - "../ejercicios/ejercicio-03-recorrido-escalonado-juntando-todo.md"
codigo_relacionado:
  - "../codigo/ejercicio-03.ri"
escenario_ciudad:
  - av: 1
    ca: 1
    flores: 1
    papeles: 1
  - av: 5
    ca: 3
    flores: 2
---

# Solución: recorrido escalonado juntando todas las flores y papeles

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-03-recorrido-escalonado-juntando-todo.md`](../ejercicios/ejercicio-03-recorrido-escalonado-juntando-todo.md).

## Análisis

`RecorrerFila` hace un "vaivén" de ida y vuelta con `pasos` pasos de largo, juntando en cada esquina que pisa, y usa dos giros de 270° (`Izquierda`, tres `derecha`) para quedar mirando en la dirección opuesta antes de volver. El driver llama a esto 9 veces reduciendo `pasos` en 2 cada vez y desplazándose 2 calles hacia arriba, dibujando el escalón decreciente de la figura.

## Estrategia

1. `JuntarEsquina(ES totalF, ES totalP)`: toma todas las flores y todos los papeles de la esquina actual, sumándolos a los acumuladores.
2. `Izquierda`: gira 270° (tres `derecha` = un giro a la izquierda), proceso sin parámetros.
3. `RecorrerFila(E pasos, ES totalF, ES totalP)`: junta la esquina de partida, avanza `pasos` veces juntando en cada una, gira dos veces con un paso extra entre giros (para desplazarse a la fila de vuelta), recorre `pasos` veces de regreso juntando, y termina con otro giro más un paso — dejando al robot listo para la siguiente fila más corta.
4. Driver: arranca con `pasos := 18`, gira una vez (queda mirando hacia avenidas crecientes), y repite 9 veces `RecorrerFila` reduciendo `pasos` en 2 y subiendo 2 calles con `Pos(1,PosCa+2)` entre una fila y la siguiente. Al final informa los dos totales acumulados.

## Código relacionado

```rinfo
programa EjAdic3

procesos

  {Junta TODO lo de la esquina y acumula en contadores}
  proceso JuntarEsquina (ES totalF: numero; ES totalP: numero)
  comenzar
    mientras HayFlorEnLaEsquina
      tomarFlor
      totalF := totalF + 1
    mientras HayPapelEnLaEsquina
      tomarPapel
      totalP := totalP + 1
  fin

  proceso Izquierda
  comenzar
    repetir 3
      derecha
  fin
  proceso RecorrerFila (E pasos: numero; ES totalF: numero; ES totalP: numero)
  comenzar
    JuntarEsquina(totalF, totalP)

    repetir pasos
      mover
      JuntarEsquina(totalF, totalP)

    Izquierda
    mover
    JuntarEsquina(totalF, totalP)
    Izquierda
    repetir pasos
      mover
      JuntarEsquina(totalF, totalP)
    Izquierda
    JuntarEsquina(totalF, totalP)
    mover
    Izquierda
  fin


areas
  ciudad: AreaC(1,1,100,100)

robots
  robot robot1
  variables
    totalFlores, totalPapeles: numero
    pasos: numero
  comenzar
    totalFlores := 0
    totalPapeles := 0

    pasos := 18
    derecha
    repetir 9
      RecorrerFila(pasos, totalFlores, totalPapeles)
      pasos := pasos - 2
      Pos(1, PosCa+ 2)

    Informar(totalFlores)
    Informar(totalPapeles)
  fin

variables
  R-info: robot1

comenzar
  AsignarArea(R-info, ciudad)
  Iniciar(R-info, 1, 1)
fin
```

Código completo: [`../codigo/ejercicio-03.ri`](../codigo/ejercicio-03.ri)

## Corrección aplicada durante esta organización

El código acumulaba `totalFlores`/`totalPapeles` correctamente vía parámetros `ES`, pero nunca los informaba — el `comenzar...fin` del robot terminaba después del `repetir 9` sin ningún `Informar`, a pesar de que el enunciado pide explícitamente "al finalizar el recorrido debe informar la cantidad total". Se agregaron `Informar(totalFlores)` e `Informar(totalPapeles)` al final, sin tocar el resto de la lógica (que ya calculaba los totales correctamente).

## Escenario de prueba

El escenario carga 1 flor y 1 papel en (1,1), más 2 flores en (5,3). El programa informa `3` flores y `1` papel. Las dos esquinas caen adentro del escalón: (1,1) en la primera fila y (5,3) en la segunda.

## Casos límite

- El recorrido cubre un rincón del mapa, no la ciudad entera. La primera fila va de la avenida 1 a la 19 sobre las calles 1 y 2. Cada fila siguiente sube dos calles y se acorta dos avenidas. La novena y última va de la avenida 1 a la 3, sobre las calles 17 y 18. Lo que esté fuera de ese escalón no se junta nunca.
- El escalón no termina en una sola esquina: `pasos` baja de 18 a 2 en nueve filas y nunca llega a 0. Para cerrar en punta harían falta diez filas.
- La vuelta de cada fila no repite la calle de ida, pasa por la de arriba. Por eso cada fila se come dos calles y el `Pos(1,PosCa+2)` salta de a dos.

## Errores frecuentes

- Usar `derecha` donde va `Izquierda`. Los tres `derecha` del proceso equivalen a un giro a la izquierda, que es el que manda al robot hacia la calle de arriba. Con un solo `derecha` gira para el lado contrario, busca la calle 0 y se sale de la ciudad en el primer `mover` de la vuelta.
- Restar 1 a `pasos` en vez de 2. No da error, pero el escalón se angosta de a una avenida por fila y deja de coincidir con la figura del enunciado.
- Terminar sin los dos `Informar`. Los totales quedan acumulados en `totalFlores` y `totalPapeles`, pero el enunciado pide mostrarlos y nadie los ve.

## Complejidad

O(1) respecto al tamaño de la ciudad: el recorrido tiene una longitud fija (suma de 18+16+...+2 pasos por ida y vuelta), independiente de las dimensiones de `AreaC`.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-03-recorrido-escalonado-juntando-todo.md`](../ejercicios/ejercicio-03-recorrido-escalonado-juntando-todo.md)
- Código: [`../codigo/ejercicio-03.ri`](../codigo/ejercicio-03.ri)
- Versión guiada: [`../practica-guiada.md`](../practica-guiada.md)
