---
id: "EPA-U06-EJ04-SOLUCION"
titulo: "Solución: recorridos de la figura 6.6 reutilizando el proceso rectángulo"
slug: "ejercicio-04-recorridos-de-rectangulos-con-proceso-parametrizado"
tipo: "solucion"
unidad: 6
tema: "parametros-de-entrada"
subtemas:
  - "declaracion-de-parametros"
  - "comunicacion-entre-modulos"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 6-Parametros de Entrada.pdf"
    paginas: "1-20"
relacionados:
  - "../ejercicios/ejercicio-04-recorridos-de-rectangulos-con-proceso-parametrizado.md"
  - "../soluciones/ejercicio-03-rectangulo-con-ancho-y-largo-parametrizados.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_4A"
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_4B"
---

# Solución: recorridos de la figura 6.6 reutilizando el proceso rectángulo

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-04-recorridos-de-rectangulos-con-proceso-parametrizado.md`](../ejercicios/ejercicio-04-recorridos-de-rectangulos-con-proceso-parametrizado.md).

## Análisis

Igual que en el ejercicio 2, cada rectángulo devuelve al robot a su esquina de partida y orientación original al cerrar (dos pares de lados con cuatro giros de 90° suman 360°). Eso permite encadenar varios rectángulos con `Pos(PosAv+1,PosCa+2)` entre cada uno, desplazando siempre una avenida a la derecha y dos calles hacia arriba, mientras se ajustan las dimensiones para el siguiente:

- **Variante A (recorrido a):** el ancho decrece de a 2 en cada rectángulo (`numer:=-2`): 5, 3, 1; el largo queda fijo en 1. Esto produce rectángulos anchos y bajos, cada vez más angostos a medida que se sube — coincide con el recorrido a) de la figura 6.6 (ancho decreciente hacia arriba).
- **Variante B (recorrido b):** el ancho queda fijo en 1 (una columna angosta) mientras el largo decrece de a 4 en cada rectángulo (`numer:=-4`): 15, 11, 7, 3. Esto produce una columna delgada de rectángulos cada vez menos altos — coincide con el recorrido b) (columna angosta).

## Estrategia

**Variante A:**

1. Inicializar `anchx := 5`, `largx := 1`, `numer := -2`.
2. Repetir 3 veces: invocar `rectangulo(anchx,largx)`, reposicionar con `Pos(PosAv+1,PosCa+2)`, y actualizar `anchx := anchx + numer`.

**Variante B:**

1. Inicializar `anchx := 1`, `largx := 15`, `numer := -4`.
2. Repetir 4 veces: invocar `rectangulo(anchx,largx)`, reposicionar con `Pos(PosAv+1,PosCa+2)`, y actualizar `largx := largx + numer`.

## Código relacionado

### Variante A — recorrido a) de la figura 6.6

```rinfo
programa  parametros
procesos
  proceso rectangulo(E ancho:numero; E largo:numero)
  comenzar
    repetir 2
      repetir largo
        mover
      derecha
      repetir ancho
        mover
      derecha
  fin
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  variables
    anchx:numero
    largx:numero
    numer:numero
  comenzar
    numer:=-2
    anchx:=5
    largx:=1
    repetir 3
      rectangulo(anchx,largx)
      Pos(PosAv+1,PosCa+2)
      anchx:=anchx+numer 
  fin
variables
  robin: robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-06/Cap6_Preg_4A`](../codigo/soluciones/capitulo-06/Cap6_Preg_4A)

### Variante B — recorrido b) de la figura 6.6

```rinfo
programa  parametros
procesos
  proceso rectangulo(E ancho:numero; E largo:numero)
  comenzar
    repetir 2
      repetir largo
        mover
      derecha
      repetir ancho
        mover
      derecha
  fin
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  variables
    anchx:numero
    largx:numero
    numer:numero
  comenzar
    numer:=-4
    anchx:=1
    largx:=15
    repetir 4
      rectangulo(anchx,largx)
      Pos(PosAv+1,PosCa+2)
      largx:=largx+numer 
  fin
variables
  robin: robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-06/Cap6_Preg_4B`](../codigo/soluciones/capitulo-06/Cap6_Preg_4B)

## Escenario de prueba

Ciudad vacía, sin flores ni papeles. La variante A dibuja tres rectángulos de 1 calle de alto y 5, 3 y 1 avenidas de ancho. La B dibuja cuatro de 1 avenida de ancho y 15, 11, 7 y 3 calles de alto. Las dos arrancan en (1,1) y suben de a una avenida y dos calles.

## Casos límite

- El `Pos` también corre después del último rectángulo. El robot termina parado en (4,7) en la variante A y en (5,9) en la B, sin dibujar nada ahí.
- La dimensión que achica `numer` termina valiendo -1 en las dos variantes: `anchx` en la A, `largx` en la B. Nadie la vuelve a usar, así que no se nota.

## Errores frecuentes

- Restarle `numer` a la dimensión equivocada. En la variante A el largo está fijo en 1 y el que achica es `anchx`. Si le restás a `largx`, el segundo rectángulo arranca con largo -1 y el robot directamente no traza esos lados.
- Olvidar el `Pos` entre invocaciones. Los tres o cuatro rectángulos se dibujan uno encima del otro desde (1,1).

## Complejidad

Cada variante dibuja una cantidad fija de rectángulos (3 en A, 4 en B): O(n) en la cantidad de rectángulos, con un costo de trazado proporcional a `ancho + largo` en cada uno.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-04-recorridos-de-rectangulos-con-proceso-parametrizado.md`](../ejercicios/ejercicio-04-recorridos-de-rectangulos-con-proceso-parametrizado.md)
- Código: [`../codigo/soluciones/capitulo-06/Cap6_Preg_4A`](../codigo/soluciones/capitulo-06/Cap6_Preg_4A), [`../codigo/soluciones/capitulo-06/Cap6_Preg_4B`](../codigo/soluciones/capitulo-06/Cap6_Preg_4B)
- Proceso base: [ejercicio 3](../ejercicios/ejercicio-03-rectangulo-con-ancho-y-largo-parametrizados.md)
