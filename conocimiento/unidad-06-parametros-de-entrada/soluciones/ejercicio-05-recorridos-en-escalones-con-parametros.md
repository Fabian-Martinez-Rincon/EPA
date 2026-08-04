---
id: "EPA-U06-EJ05-SOLUCION"
titulo: "Solución: cuatro recorridos en escalones de la figura 6.7"
slug: "ejercicio-05-recorridos-en-escalones-con-parametros"
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
  - "../ejercicios/ejercicio-05-recorridos-en-escalones-con-parametros.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_5A"
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_5B"
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_5C"
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_5D"
---

# Solución: cuatro recorridos en escalones de la figura 6.7

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-05-recorridos-en-escalones-con-parametros.md`](../ejercicios/ejercicio-05-recorridos-en-escalones-con-parametros.md).

## Análisis

Un "escalón" es una figura abierta (no un rectángulo cerrado): se avanza por un lado, se gira 90°, se avanza por el otro lado, y ahí se detiene — a diferencia del cuadrado/rectángulo de los ejercicios 1-4, que cierran con cuatro giros. Como después de un escalón el robot queda mirando en sentido contrario al que empezó (180° girado), las cuatro variantes usan un proceso auxiliar `izquierda` (dos `derecha`, o sea otros 180°) para devolver al robot a su orientación original antes de trazar el siguiente escalón, permitiendo encadenarlos en una escalera.

- **Variante A:** el proceso `rectangulo(E ancho:numero)` recibe un solo parámetro y lo usa para **ambos** lados del escalón (mismo ancho y alto) y ya incluye el `izquierda` final dentro de sí mismo. El programa principal encadena 3 escalones de tamaño decreciente (5, 4, 3), cada uno un cuadrado abierto.
- **Variantes B y C:** el proceso `rectangulo(E ancho:numero; E largo:numero)` recibe dos parámetros independientes para cada lado del escalón, y el `izquierda` se invoca aparte, desde el programa principal, después de cada escalón. Se encadenan 3 escalones donde un lado decrece (3, 2, 1) mientras el otro crece (2, 3, 4) — una escalera con proporciones cambiantes en vez de escalones cuadrados.
- **Variante D:** usa el mismo proceso de dos parámetros que B/C, pero con `ancho` y `largo` constantes (2 y 4) en las cuatro repeticiones. En vez de variar el tamaño, cambia el rumbo: traza dos escalones, gira 90° con un `derecha` suelto (distinto del `izquierda` que reorienta después de cada escalón) y traza otros dos escalones en la nueva dirección, formando una escalera con un quiebre a mitad de camino en vez de una progresión de tamaños en línea recta.

## Estrategia

**Variante A:**

1. Declarar `proceso rectangulo(E ancho:numero)` que avance `ancho`, gire a la derecha, avance `ancho` de nuevo, gire a la derecha y gire 180° más (`izquierda`) para restaurar la orientación original.
2. Desde el programa principal, repetir 3 veces: invocar `rectangulo(anchx)` y decrementar `anchx` en 1 (arrancando en 5).

**Variantes B y C:**

1. Declarar `proceso rectangulo(E ancho:numero; E largo:numero)` que avance `ancho`, gire a la derecha, avance `largo` y gire a la derecha (queda 180° girado).
2. Declarar `proceso izquierda` (dos `derecha`) para restaurar la orientación.
3. Desde el programa principal, repetir 3 veces: invocar `rectangulo(anchx,largx)`, invocar `izquierda`, decrementar `anchx` en 1 e incrementar `largx` en 1 (arrancando en 3 y 2 respectivamente).

**Variante D:**

1. Reutilizar los mismos procesos `rectangulo(E ancho; E largo)` e `izquierda`.
2. Reposicionar en (1,5); repetir 2 veces: invocar `rectangulo(anchx,largx)` e `izquierda`, con `anchx:=2` y `largx:=4` fijos.
3. Girar una vez más a la derecha (cambiando de rumbo) y repetir 2 veces más el mismo par de invocaciones.

## Código relacionado

### Variante A

```
programa  parametros
procesos
  proceso rectangulo(E ancho:numero)
  comenzar
    repetir 2
      repetir ancho
        mover
      derecha
    izquierda
  fin
  proceso izquierda
  comenzar
    repetir 2
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
    numer:=-1
    anchx:=5
    largx:=5 
    repetir 3
      rectangulo(anchx)
      anchx:=anchx+numer
  fin
variables
  robin: robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-06/Cap6_Preg_5A`](../codigo/soluciones/capitulo-06/Cap6_Preg_5A)

### Variante B

```
programa  parametros
procesos
  proceso rectangulo(E ancho:numero;E largo:numero)
  comenzar
    repetir ancho
      mover
    derecha
    repetir largo
      mover
    derecha
  fin
  proceso izquierda
  comenzar
    repetir 2
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
    numer:=-1
    anchx:=3
    largx:=2
    repetir 3
      rectangulo(anchx,largx)
      izquierda
      anchx:=anchx+numer
      largx:=largx+1
  fin
variables
  robin: robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-06/Cap6_Preg_5B`](../codigo/soluciones/capitulo-06/Cap6_Preg_5B)

### Variante C

Este archivo es, cuadra por cuadra, el mismo código que la variante B (ver nota más abajo).

```
programa  parametros
procesos
  proceso rectangulo(E ancho:numero;E largo:numero)
  comenzar
    repetir ancho
      mover
    derecha
    repetir largo
      mover
    derecha
  fin
  proceso izquierda
  comenzar
    repetir 2
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
    numer:=-1
    anchx:=3
    largx:=2
    repetir 3
      rectangulo(anchx,largx)
      izquierda
      anchx:=anchx+numer
      largx:=largx+1
  fin
variables
  robin: robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-06/Cap6_Preg_5C`](../codigo/soluciones/capitulo-06/Cap6_Preg_5C)

### Variante D

```
programa  parametros
procesos
  proceso rectangulo(E ancho:numero;E largo:numero)
  comenzar
    repetir ancho
      mover
    derecha
    repetir largo
      mover
    derecha
  fin
  proceso izquierda
  comenzar
    repetir 2
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
    Pos(1,5)
    numer:=-1
    anchx:=2
    largx:=4 
    repetir 2
      rectangulo(anchx,largx)
      izquierda
    derecha
    repetir 2
      rectangulo(anchx,largx)
      izquierda
      
  fin
variables
  robin: robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-06/Cap6_Preg_5D`](../codigo/soluciones/capitulo-06/Cap6_Preg_5D)

## Nota: las variantes B y C son idénticas en el material histórico

Los archivos `Cap6_Preg_5B` y `Cap6_Preg_5C` solo difieren en el comentario `{...}` del encabezado ("(variante B)" vs. "(variante C)"); el resto del código —proceso, parámetros, valores iniciales y estructura del programa principal— es exactamente el mismo. La figura 6.7 muestra cuatro paneles (a, b, c, d) con aspecto distinto entre sí, así que es probable que en el material original la variante C debiera producir un recorrido distinto al de B y el archivo haya quedado duplicado por error de copiado. No se intentó reconstruir cuál sería el recorrido "correcto" de C, porque hacerlo implicaría inventar contenido nuevo sin evidencia (no hay ningún archivo fuente adicional ni referencia que indique qué cambio faltó); se documenta la duplicación acá para que quede claro al comparar el código con la figura.

## Escenario de prueba

Ninguna de las cuatro variantes requiere flores ni papeles precargados: alcanza con observar el recorrido en forma de escalera que traza cada una a partir de (1,1) (o de (1,5) en la variante D).

## Casos límite

- Variante A: `largx` se declara y se inicializa pero nunca se usa (el único parámetro del proceso es `ancho`); es una variable muerta, no afecta el resultado.
- Variante D: `numer` se declara y se inicializa en -1 pero tampoco se usa — `anchx` y `largx` quedan constantes durante las cuatro invocaciones a `rectangulo`, a diferencia de A/B/C donde sí cambian en cada paso.

## Errores frecuentes

- Olvidar el `izquierda` (o el giro final incluido dentro del proceso, en la variante A) entre escalón y escalón: sin restaurar la orientación, el siguiente escalón saldría en un ángulo equivocado en vez de continuar la escalera.
- Confundir el `derecha` suelto de la variante D (que cambia el rumbo general de la escalera) con el `izquierda` que reorienta después de cada escalón individual: cumplen roles distintos y no son intercambiables.

## Complejidad

Cada variante traza una cantidad fija de escalones (3 en A/B/C, 4 en D): O(n) en la cantidad de escalones, con costo proporcional a la suma de sus dos lados en cada uno.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-05-recorridos-en-escalones-con-parametros.md`](../ejercicios/ejercicio-05-recorridos-en-escalones-con-parametros.md)
- Código: [`../codigo/soluciones/capitulo-06/Cap6_Preg_5A`](../codigo/soluciones/capitulo-06/Cap6_Preg_5A), [`../codigo/soluciones/capitulo-06/Cap6_Preg_5B`](../codigo/soluciones/capitulo-06/Cap6_Preg_5B), [`../codigo/soluciones/capitulo-06/Cap6_Preg_5C`](../codigo/soluciones/capitulo-06/Cap6_Preg_5C), [`../codigo/soluciones/capitulo-06/Cap6_Preg_5D`](../codigo/soluciones/capitulo-06/Cap6_Preg_5D)
