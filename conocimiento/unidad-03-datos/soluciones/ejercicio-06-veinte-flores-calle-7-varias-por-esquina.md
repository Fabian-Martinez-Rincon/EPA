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

```
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

Cargar flores repartidas en esquinas con cantidades variables que sumen 20 (por ejemplo, 5 en la avenida 3, 5 en la avenida 6 y 10 en la avenida 9, todas en calle 7). Probado con el intérprete: con esa distribución, el programa informa la posición `(10,7)` — un paso más allá de la avenida 9, donde se recogió la última tanda de flores, consistente con que `mover` se ejecuta una vez más antes de que el `mientras` exterior vuelva a chequear la condición.

## Casos límite

- Una sola esquina con las 20 flores: el `mientras` interno las toma todas de una vez y el robot avanza sólo una esquina.
- El enunciado no exige informar `x`; el código informa la posición final en su lugar, una elección razonable ya que el enunciado no especifica qué informar.

## Errores frecuentes

- Usar `si` en vez de `mientras` para tomar las flores de la esquina, lo que dejaría flores sin recoger si hay más de una por esquina.

## Complejidad

Recorrido de hasta 100 esquinas (una calle completa), con una cantidad de tomas de flores acotada por las 20 garantizadas: O(1) respecto al tamaño de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-06-veinte-flores-calle-7-varias-por-esquina.md`](../ejercicios/ejercicio-06-veinte-flores-calle-7-varias-por-esquina.md)
- Código: [`../codigo/capitulo-3-pregunta-06.ri`](../codigo/capitulo-3-pregunta-06.ri)
