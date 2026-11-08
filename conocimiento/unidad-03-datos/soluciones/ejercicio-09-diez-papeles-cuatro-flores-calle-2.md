---
id: "EPA-U03-EJ09-SOLUCION"
titulo: "Solución: caminar la calle 2 hasta encontrar 10 papeles y 4 flores"
slug: "ejercicio-09-diez-papeles-cuatro-flores-calle-2"
tipo: "solucion"
unidad: 3
tema: "datos-y-variables"
subtemas:
  - "variables"
  - "estructuras-de-control"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 3-Datos.pdf"
    paginas: "1-21"
relacionados:
  - "../ejercicios/ejercicio-09-diez-papeles-cuatro-flores-calle-2.md"
codigo_relacionado:
  - "../codigo/capitulo-3-pregunta-09.ri"
escenario_ciudad:
  - av: 3
    ca: 2
    papeles: 10
  - av: 5
    ca: 2
    flores: 4
---

# Solución: caminar la calle 2 hasta encontrar 10 papeles y 4 flores

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-09-diez-papeles-cuatro-flores-calle-2.md`](../ejercicios/ejercicio-09-diez-papeles-cuatro-flores-calle-2.md).

## Análisis

Se usan dos contadores, `x` (papeles) e `y` (flores), y una única condición de corte `(x<10)|(y<4)`: el robot sigue caminando mientras falte alguna de las dos cantidades. Como el `mover` está al mismo nivel que las dos tomas (no anidado dentro de ninguna condición), no hay riesgo del bug de loop infinito visto en los ejercicios 5 y 8.

## Estrategia

1. Posicionar el robot en (1,2) y girar a la derecha.
2. Mientras `(x<10)|(y<4)`: drenar los papeles y las flores de la esquina actual; avanzar.
3. Repetir el mismo procesamiento (sin avanzar) para la esquina final, dado que el enunciado garantiza que las cantidades se completan dentro de la calle.
4. Informar la posición final.

## Código relacionado

```rinfo
programa prueba
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  variables
    x: numero
    y: numero
    z:numero
  comenzar
    Pos(1,2)
    x:=0
    y:=0
    derecha
    mientras(x<10)|(y<4)
      mientras(HayPapelEnLaEsquina)
        tomarPapel
        x:=x+1
      mientras(HayFlorEnLaEsquina)
        tomarFlor
        y:=y+1
      mover
    mientras(x<10)|(y<4)
      mientras(HayPapelEnLaEsquina)
        tomarPapel
        x:=x+1
      mientras(HayFlorEnLaEsquina)
        tomarFlor
        y:=y+1
    Informar((PosAv),PosCa)
  fin
variables
  robin:robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/capitulo-3-pregunta-09.ri`](../codigo/capitulo-3-pregunta-09.ri)

## Escenario de prueba

Poné los papeles y las flores en esquinas distintas de la calle 2: 10 papeles en la avenida 3 y 4 flores en la avenida 5. El robot informa `(6,2)`. Completó las flores en la avenida 5 y el `mover` del final del cuerpo lo corrió una esquina más.

## Casos límite

- El corte es `(x<10)|(y<4)`: mientras falte cualquiera de las dos cantidades, el robot sigue. Con `&` en lugar de `|` frenaría apenas completa una sola de las dos.
- El segundo `mientras(x<10)|(y<4)`, el que va sin `mover`, no se ejecuta nunca. El primero sale justo cuando esa condición se vuelve falsa, y entre uno y otro no hay nada que cambie `x` ni `y`.
- Si las cantidades recién se completan en la avenida 100, el `mover` del final del cuerpo deja al robot fuera de la ciudad y el programa corta con error, sin informar nada.

## Errores frecuentes

- Usar un solo contador para las dos cosas. Con `x` sumando papeles y flores juntos, 14 papeles y ninguna flor te darían por cumplido el pedido.
- Resolverlo con dos recorridos seguidos, primero los papeles y después las flores. El segundo arranca donde terminó el primero, así que las flores que quedaron atrás no las ve nunca.

## Complejidad

Recorrido de hasta 100 esquinas (una calle completa): O(1) respecto al tamaño de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-09-diez-papeles-cuatro-flores-calle-2.md`](../ejercicios/ejercicio-09-diez-papeles-cuatro-flores-calle-2.md)
- Código: [`../codigo/capitulo-3-pregunta-09.ri`](../codigo/capitulo-3-pregunta-09.ri)
