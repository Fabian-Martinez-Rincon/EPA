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

```
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

Cargar 10 papeles en una esquina y 4 flores en otra, ambas dentro de la calle 2 (por ejemplo, 10 papeles en avenida 3 y 4 flores en avenida 5). Probado con el intérprete: con esa distribución el programa termina en la posición `(6,2)`, un paso después de recoger las flores en la avenida 5, consistente con el patrón de "un paso de más" propio de `mientras` en R-info.

## Casos límite

- El segundo `mientras(x<10)|(y<4)` (sin `mover`, pensado para procesar "la última esquina") en la práctica sólo importa si el primer bucle deja de moverse justo al satisfacer la condición en la última esquina de la calle; en el resto de los casos no hace nada (la condición ya es falsa y su cuerpo ni se ejecuta), verificado con el intérprete.
- Al igual que en el ejercicio 4, si las cantidades garantizadas sólo se completan en la avenida 100 exacta, el `mover` incondicional del primer bucle podría llevar al robot a la avenida 101 (fuera de la ciudad); es el mismo riesgo inherente a este estilo de recorrido con `mientras`, ya presente en los ejemplos de la teoría, y no es un error propio de este archivo.

## Errores frecuentes

- Usar una condición de corte para cada tipo de objeto por separado (dos `mientras` anidados) en vez de una sola condición combinada con `|`, lo que complicaría innecesariamente el control del recorrido.

## Complejidad

Recorrido de hasta 100 esquinas (una calle completa): O(1) respecto al tamaño de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-09-diez-papeles-cuatro-flores-calle-2.md`](../ejercicios/ejercicio-09-diez-papeles-cuatro-flores-calle-2.md)
- Código: [`../codigo/capitulo-3-pregunta-09.ri`](../codigo/capitulo-3-pregunta-09.ri)
