---
id: "EPA-U06-EJ06-SOLUCION"
titulo: "Solución: recorrer avenidas con el número como parámetro"
slug: "ejercicio-06-recorrer-avenidas-con-numero-parametrizado"
tipo: "solucion"
unidad: 6
tema: "parametros-de-entrada"
subtemas:
  - "declaracion-de-parametros"
  - "comunicacion-entre-modulos"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "parcial"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 6-Parametros de Entrada.pdf"
    paginas: "1-20"
relacionados:
  - "../ejercicios/ejercicio-06-recorrer-avenidas-con-numero-parametrizado.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_6A"
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_6B"
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_6C"
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_6D"
---

# Solución: recorrer avenidas con el número como parámetro

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-06-recorrer-avenidas-con-numero-parametrizado.md`](../ejercicios/ejercicio-06-recorrer-avenidas-con-numero-parametrizado.md).

## Análisis

Recorrer "una avenida" significa moverse manteniendo la avenida fija y la calle variable. Como el robot arranca sin girar (orientación por defecto), `mover` ya incrementa `PosCa` — no hace falta ningún `derecha` para este eje. El proceso base (6.a) se limita a reposicionar con `Pos(avenida,PosCa)` (fija la avenida pedida, conserva la calle actual) y avanzar 99 veces, recorriendo así las 99 cuadras entre la calle 1 y la 100.

Las partes b, c y d reutilizan ese mismo proceso envolviéndolo en un `repetir` adicional que, en cada vuelta, recorre la avenida actual y salta a la siguiente con `Pos(PosAv±k,1)`:

- **6.b:** arranca en la avenida 1 y repite 99 veces "recorrer la avenida actual, saltar a la próxima" (paso de a 1 avenida).
- **6.c:** arranca en la avenida 5 y repite 10 veces el mismo patrón (paso de a 1 avenida).
- **6.d:** arranca en la avenida 2 y repite 49 veces el mismo patrón, saltando de a 2 avenidas para quedarse en las pares.

## Estrategia

**6.a:**

1. Declarar `proceso JuntarFlor(E avenida:numero; E NumFlores:numero)`.
2. Reposicionar con `Pos(avenida,PosCa)` (cambia solo la avenida, conserva la calle actual).
3. Avanzar 99 veces (recorre la avenida completa, calle 1 a 100).

**6.b/6.c/6.d:**

1. Reposicionar al inicio de la primera avenida a recorrer con `Pos(avenida,1)`.
2. Repetir *N* veces: avanzar 99 veces (recorrer la avenida actual) y saltar a la siguiente avenida con `Pos(PosAv+k,1)`.

## Código relacionado

### 6.a) — proceso base

```
programa  parametros
procesos
  proceso izquierda
  comenzar
    repetir 2
      derecha
  fin
  proceso JuntarFlor(E avenida:numero;E NumFlores:numero)
  variables
    CantFlores:numero
  comenzar
    Pos(avenida,PosCa)
    repetir 99
      mover
  fin
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  variables
    avenidad:numero
    NFlores:numero
  comenzar
    NFlores:=4
    avenidad:=19
    JuntarFlor(avenidad,NFlores)
  fin
variables
  robin: robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-06/Cap6_Preg_6A`](../codigo/soluciones/capitulo-06/Cap6_Preg_6A)

### 6.b) — todas las avenidas

```
programa  parametros
procesos
  proceso izquierda
  comenzar
    repetir 2
      derecha
  fin
  proceso JuntarFlor(E avenida:numero;E NumFlores:numero)
  variables
    CantFlores:numero
    num:numero
  comenzar
    num:=0
    Pos(avenida,1)
    repetir 99
      repetir 99
        mover
      Pos(PosAv+1,1)
  fin
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  variables
    avenidad:numero
    NFlores:numero
  comenzar
    NFlores:=4
    avenidad:=1
    JuntarFlor(avenidad,NFlores)
  fin
variables
  robin: robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-06/Cap6_Preg_6B`](../codigo/soluciones/capitulo-06/Cap6_Preg_6B)

### 6.c) — avenidas 5 a 15

```
programa  parametros
procesos
  proceso izquierda
  comenzar
    repetir 2
      derecha
  fin
  proceso JuntarFlor(E avenida:numero;E NumFlores:numero)
  variables
    CantFlores:numero
    num:numero
  comenzar
    num:=0
    Pos(avenida,1)
    repetir 10
      repetir 99
        mover
      Pos(PosAv+1,1)
  fin
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  variables
    avenidad:numero
    NFlores:numero
  comenzar
    NFlores:=4
    avenidad:=5
    JuntarFlor(avenidad,NFlores)
  fin
variables
  robin: robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-06/Cap6_Preg_6C`](../codigo/soluciones/capitulo-06/Cap6_Preg_6C)

### 6.d) — avenidas pares

```
programa  parametros
procesos
  proceso izquierda
  comenzar
    repetir 2
      derecha
  fin
  proceso JuntarFlor(E avenida:numero;E NumFlores:numero)
  variables
    CantFlores:numero
    num:numero
  comenzar
    num:=0
    Pos(avenida,1)
    repetir 49
      repetir 99
        mover
      Pos(PosAv+2,1)
  fin
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  variables
    avenidad:numero
    NFlores:numero
  comenzar
    NFlores:=4
    avenidad:=2
    JuntarFlor(avenidad,NFlores)
  fin
variables
  robin: robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-06/Cap6_Preg_6D`](../codigo/soluciones/capitulo-06/Cap6_Preg_6D)

## Alcance no corregido: la última avenida pedida queda sin recorrer en 6.b, 6.c y 6.d

Las tres partes que encadenan avenidas (6.b, 6.c, 6.d) siguen el mismo patrón: `repetir N { recorrer avenida actual (99 movimientos); Pos(PosAv+k,1) }`. Ese `Pos` final de cada vuelta deja al robot **parado** en la siguiente avenida, pero sin recorrerla — esa avenida recién se recorre en la vuelta *siguiente* del `repetir`. Como el contador `N` se calculó para completar exactamente las avenidas recorridas y no las visitadas, la última avenida pedida en cada enunciado queda solo "alcanzada" (el robot llega a su esquina de partida) pero no "recorrida" (nunca se ejecuta el `repetir 99 mover` para ella):

- **6.b** ("todas las avenidas de la ciudad"): con `repetir 99` se recorren las avenidas 1 a 99; la avenida 100 se alcanza pero no se recorre. Haría falta `repetir 100` para cubrir las 100 avenidas.
- **6.c** ("avenidas 5, 6, 7 … 15", 11 avenidas): con `repetir 10` se recorren las avenidas 5 a 14; la avenida 15 se alcanza pero no se recorre. Haría falta `repetir 11`.
- **6.d** ("avenidas pares de la ciudad", 50 avenidas de la 2 a la 100): con `repetir 49` se recorren las avenidas 2 a 98; la avenida 100 se alcanza pero no se recorre. Haría falta `repetir 50`.

Se documenta acá en vez de corregirse porque, a diferencia de los bugs puntuales de otros ejercicios de esta unidad, este patrón se repite igual en las tres variantes — no es un error de una palabra suelta sino una cuestión de cómo se calculó el límite del `repetir` en el material original (mismo criterio que se usó en la unidad 2 para el ejercicio 9, donde también se documentó un límite de recorrido que no llega exactamente al último elemento pedido, en vez de reescribir la fórmula del conteo).

## Nota: el proceso `JuntarFlor` no junta flores en ninguna de las cuatro variantes

A pesar de su nombre y de recibir un parámetro `NumFlores`, el proceso de las cuatro partes solo mueve al robot; nunca consulta `HayFlorEnLaEsquina` ni llama a `tomarFlor`. Las variables `NumFlores`, `CantFlores` y `num` quedan declaradas pero sin usar. Esto no contradice el enunciado del ejercicio 6 (que en sus cuatro partes solo pide "recorrer" avenidas, sin mencionar flores), pero es evidencia de que el proceso fue copiado de otro ejercicio de la ejercitación (probablemente el 7, centrado en juntar flores) sin terminar de adaptarlo. No se quitaron los parámetros/variables sin uso ni se agregó lógica de recolección, porque el enunciado de este ejercicio no la pide y hacerlo sería agregar comportamiento nuevo no solicitado.

## Escenario de prueba

No requiere flores ni papeles precargados: los cuatro programas solo mueven al robot (ver nota anterior). Alcanza con observar, para cada variante, qué avenidas efectivamente recorre según el análisis de esta solución.

## Casos límite

- 6.a) invocado con la avenida 1 mientras el robot está parado en cualquier calle: conserva esa calle (`Pos(avenida,PosCa)`) y recorre desde ahí hasta la calle 100, no necesariamente las 99 cuadras completas si no arranca en la calle 1.
- Ver la sección anterior para el límite compartido por 6.b/6.c/6.d (última avenida pedida no recorrida).

## Errores frecuentes

- Usar `derecha` antes de recorrer la avenida en 6.a): no hace falta, porque la orientación inicial del robot ya avanza a lo largo de las calles cuando la avenida está fija.
- Calcular la cantidad de repeticiones como "diferencia entre avenida final e inicial" en vez de "diferencia más uno", que es precisamente el error compartido por 6.b/6.c/6.d descrito arriba.

## Complejidad

Cada parte recorre O(k) avenidas de 99 pasos cada una: 6.a) es O(1) (una sola avenida); 6.b), 6.c) y 6.d) son O(k) en la cantidad de avenidas encadenadas, con un costo total de `99k` pasos.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-06-recorrer-avenidas-con-numero-parametrizado.md`](../ejercicios/ejercicio-06-recorrer-avenidas-con-numero-parametrizado.md)
- Fuente original: [`../fuentes/Capitulo 6-Parametros de Entrada.pdf`](<../fuentes/Capitulo 6-Parametros de Entrada.pdf>)
- Código: [`../codigo/soluciones/capitulo-06/Cap6_Preg_6A`](../codigo/soluciones/capitulo-06/Cap6_Preg_6A), [`../codigo/soluciones/capitulo-06/Cap6_Preg_6B`](../codigo/soluciones/capitulo-06/Cap6_Preg_6B), [`../codigo/soluciones/capitulo-06/Cap6_Preg_6C`](../codigo/soluciones/capitulo-06/Cap6_Preg_6C), [`../codigo/soluciones/capitulo-06/Cap6_Preg_6D`](../codigo/soluciones/capitulo-06/Cap6_Preg_6D)
