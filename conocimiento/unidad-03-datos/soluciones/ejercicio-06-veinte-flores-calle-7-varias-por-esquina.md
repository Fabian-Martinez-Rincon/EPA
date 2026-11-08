---
id: "EPA-U03-EJ06-SOLUCION"
titulo: "Solución: caminar la calle 7 hasta encontrar 20 flores (varias por esquina)"
slug: "ejercicio-06-veinte-flores-calle-7-varias-por-esquina"
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
  - "../ejercicios/ejercicio-06-veinte-flores-calle-7-varias-por-esquina.md"
codigo_relacionado:
  - "../codigo/capitulo-3-pregunta-06.ri"
escenario_ciudad:
  - av: 3
    ca: 7
    flores: 5
  - av: 6
    ca: 7
    flores: 5
  - av: 9
    ca: 7
    flores: 10
---

# Solución: caminar la calle 7 hasta encontrar 20 flores (varias por esquina)

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-06-veinte-flores-calle-7-varias-por-esquina.md`](../ejercicios/ejercicio-06-veinte-flores-calle-7-varias-por-esquina.md).

## Análisis

Como ahora una esquina puede tener varias flores, no alcanza con `si(HayFlorEnLaEsquina)`: hay que drenar toda la esquina con un `mientras(HayFlorEnLaEsquina)` interno antes de avanzar, para no perderse flores adicionales en la misma esquina. Como el enunciado garantiza que existen 20 flores en total, el `mientras(x<20)` exterior alcanza como única condición de corte.

## Estrategia

1. Posicionar el robot en (1,7) y girar a la derecha.
2. Mientras `x<20`: tomar todas las flores de la esquina actual (pueden ser 0, 1 o varias), contándolas en `x`; avanzar.
3. Informar la posición final.

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
  comenzar
    Pos(1,7)
    x:=0
    derecha
    mientras(x<20)
      mientras(HayFlorEnLaEsquina)
        tomarFlor
        x:=x+1
      mover
    Informar(PosAv,PosCa)
  fin
variables
  robin:robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/capitulo-3-pregunta-06.ri`](../codigo/capitulo-3-pregunta-06.ri)

## Escenario de prueba

Repartí las 20 flores en pocas esquinas, con cantidades distintas: 5 en la avenida 3, 5 en la 6 y 10 en la 9, todas en la calle 7. El robot informa la posición `(10,7)`. Levantó la última tanda en la avenida 9 y el `mover` del final del cuerpo lo dejó una esquina más adelante.

## Casos límite

- Las 20 flores en una sola esquina: el `mientras` interno las levanta todas de un saque. Con las 20 en la avenida 1, el robot informa `(2,7)`.
- Si en total hubiera menos de 20, el programa no terminaría bien: el robot camina hasta salirse de la ciudad, igual que en el ejercicio 4. Por eso el enunciado las garantiza.

## Errores frecuentes

- Usar `si(HayFlorEnLaEsquina)` en vez de `mientras`. Con 5 flores en la esquina te llevás una sola y el robot sigue de largo dejando cuatro atrás.

## Complejidad

Recorrido de hasta 100 esquinas (una calle completa), con una cantidad de tomas de flores acotada por las 20 garantizadas: O(1) respecto al tamaño de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-06-veinte-flores-calle-7-varias-por-esquina.md`](../ejercicios/ejercicio-06-veinte-flores-calle-7-varias-por-esquina.md)
- Código: [`../codigo/capitulo-3-pregunta-06.ri`](../codigo/capitulo-3-pregunta-06.ri)
