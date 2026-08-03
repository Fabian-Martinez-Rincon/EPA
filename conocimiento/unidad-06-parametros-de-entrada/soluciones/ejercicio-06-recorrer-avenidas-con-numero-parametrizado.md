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
estado: "completo"
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

Las partes b, c y d reutilizan ese mismo proceso envolviéndolo en un `repetir` adicional que, en cada vuelta, recorre la avenida actual y salta a la siguiente con `Pos(PosAv±k,1)`. El contador del `repetir` debe ser exactamente la cantidad de avenidas a recorrer (no la cantidad de "saltos" entre avenidas, que es uno menos): recorrer *N* avenidas requiere *N* vueltas, aunque la última vuelta no necesite saltar a ninguna parte después. Por eso el salto final queda protegido con `si(PosAv<100)`, para no intentar un `Pos` fuera del área de 100×100 cuando la avenida recorrida es la 100:

- **6.b:** arranca en la avenida 1 y repite 100 veces "recorrer la avenida actual, saltar a la próxima si queda alguna" (paso de a 1 avenida) — cubre las 100 avenidas de la ciudad.
- **6.c:** arranca en la avenida 5 y repite 11 veces el mismo patrón (paso de a 1 avenida) — cubre las avenidas 5 a 15 (11 avenidas; como ninguna vuelta llega a la avenida 100, ninguna vuelta necesita el guard y de hecho no lo tiene, ver "Corrección aplicada").
- **6.d:** arranca en la avenida 2 y repite 50 veces el mismo patrón, saltando de a 2 avenidas para quedarse en las pares — cubre las 50 avenidas pares de la 2 a la 100.

## Estrategia

**6.a:**

1. Declarar `proceso JuntarFlor(E avenida:numero; E NumFlores:numero)`.
2. Reposicionar con `Pos(avenida,PosCa)` (cambia solo la avenida, conserva la calle actual).
3. Avanzar 99 veces (recorre la avenida completa, calle 1 a 100).

**6.b/6.c/6.d:**

1. Reposicionar al inicio de la primera avenida a recorrer con `Pos(avenida,1)`.
2. Repetir *N* veces, donde *N* es la cantidad de avenidas a recorrer (no la cantidad de saltos entre ellas): avanzar 99 veces (recorrer la avenida actual) y, si todavía no se llegó al borde de la ciudad (`PosAv<100`), saltar a la siguiente avenida con `Pos(PosAv+k,1)`. El guard evita un `Pos` fuera del área de 100×100 en la última vuelta cuando esa vuelta recorre justo la avenida 100.

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
    repetir 100
      repetir 99
        mover
      si(PosAv<100)
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
    repetir 11
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
    repetir 50
      repetir 99
        mover
      si(PosAv<100)
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

## Corrección aplicada: la última avenida pedida no se recorría en 6.b, 6.c y 6.d

Las tres partes que encadenan avenidas (6.b, 6.c, 6.d) seguían el mismo patrón: `repetir N { recorrer avenida actual (99 movimientos); Pos(PosAv+k,1) }`. Ese `Pos` final de cada vuelta deja al robot **parado** en la siguiente avenida, pero sin recorrerla — esa avenida recién se recorre en la vuelta *siguiente* del `repetir`. El contador `N` original se había calculado como la cantidad de *saltos* entre avenidas en vez de la cantidad de avenidas a recorrer (que es uno más), así que la última avenida pedida en cada enunciado quedaba solo "alcanzada" (el robot llegaba a su esquina de partida) pero no "recorrida" (nunca se ejecutaba el `repetir 99 mover` para ella).

**Fix aplicado** (mismo patrón en los tres archivos, `codigo/soluciones/capitulo-06/Cap6_Preg_6B`, `6C`, `6D`): se aumentó en 1 el contador del `repetir` exterior para que cuente avenidas en vez de saltos. Al probar el cambio contra el intérprete apareció un problema adicional no anticipado: en 6.b y 6.d la última vuelta del `repetir` ahora recorre justo la avenida 100 (el borde de la ciudad de 100×100), y el `Pos(PosAv+k,1)` incondicional al final de cada vuelta intentaba saltar a la avenida 101 (6.b) o 102 (6.d), fuera del área — el intérprete cortaba la ejecución con `Pos(101,1) está fuera del área` / `Pos(102,1) está fuera del área` y el programa nunca llegaba a `fin`. Por eso, además de subir el contador, ese `Pos` final se protegió con `si(PosAv<100)` para que no se ejecute cuando la vuelta que acaba de terminar ya recorrió la avenida 100:

- **6.b** ("todas las avenidas de la ciudad", 100 avenidas): `repetir 99` → `repetir 100`, más `si(PosAv<100)` antes del `Pos(PosAv+1,1)`.
- **6.c** ("avenidas 5, 6, 7 … 15", 11 avenidas): `repetir 10` → `repetir 11`. No hizo falta guard: la última vuelta recorre la avenida 15 y el salto siguiente sería a la avenida 16, que sigue dentro del área de 100×100, así que no rompe nada.
- **6.d** ("avenidas pares de la ciudad", 50 avenidas de la 2 a la 100): `repetir 49` → `repetir 50`, más `si(PosAv<100)` antes del `Pos(PosAv+2,1)`.

**Evidencia de las pruebas** (ciudad y bolsa vacías, vía el intérprete de R-info de Academia-Fabo en `http://localhost:3000/api/run-rinfo`, inspeccionando los eventos `mover` para confirmar cobertura completa — no solo que el robot "llega" a la avenida final sino que la recorre entera, `ca` de 1 a 100):

- **6.b:** sin el guard, `repetir 100` solo tira `ERROR en línea 19: Pos(101,1) está fuera del área`. Con el guard: 0 errores, 10002 eventos, últimos eventos en `av:100, ca:94..100` seguidos de `fin`. Las 100 avenidas (1 a 100) aparecen con eventos `mover`, y las 100 tienen exactamente 99 movers con `ca` de 2 a 100 (recorrido completo de punta a punta) — verificado programáticamente agrupando los eventos `mover` por avenida.
- **6.c:** sin cambios de guard (no lo necesita). Con `repetir 11`: 0 errores, 1103 eventos, últimos eventos en `av:15, ca:95..100` seguidos de `pos av:16 ca:1` y `fin`. Las 11 avenidas (5 a 15) aparecen con eventos `mover`, cada una con exactamente 99 movers de `ca` 2 a 100.
- **6.d:** sin el guard, `repetir 50` tira `ERROR en línea 19: Pos(102,1) está fuera del área`. Con el guard: 0 errores, 5002 eventos, últimos eventos en `av:100, ca:94..100` seguidos de `fin`. Las 50 avenidas pares (2 a 100) aparecen con eventos `mover`, cada una con exactamente 99 movers de `ca` 2 a 100.

En los tres casos se comparó además contra la versión sin corregir: con los contadores originales (99/10/49) el patrón se repetía sin errores de ejecución, pero la última avenida pedida (100/15/100 según el caso) nunca aparecía en la lista de avenidas con 99 movers completos — quedaba solo con el evento de reposicionamiento inicial. Después del fix, las tres variantes cubren exactamente las avenidas que pide cada enunciado, sin errores de ejecución.

## Nota: el proceso `JuntarFlor` no junta flores en ninguna de las cuatro variantes

A pesar de su nombre y de recibir un parámetro `NumFlores`, el proceso de las cuatro partes solo mueve al robot; nunca consulta `HayFlorEnLaEsquina` ni llama a `tomarFlor`. Las variables `NumFlores`, `CantFlores` y `num` quedan declaradas pero sin usar. Esto no contradice el enunciado del ejercicio 6 (que en sus cuatro partes solo pide "recorrer" avenidas, sin mencionar flores), pero es evidencia de que el proceso fue copiado de otro ejercicio de la ejercitación (probablemente el 7, centrado en juntar flores) sin terminar de adaptarlo. No se quitaron los parámetros/variables sin uso ni se agregó lógica de recolección, porque el enunciado de este ejercicio no la pide y hacerlo sería agregar comportamiento nuevo no solicitado.

## Escenario de prueba

No requiere flores ni papeles precargados: los cuatro programas solo mueven al robot (ver nota anterior). Alcanza con observar, para cada variante, qué avenidas efectivamente recorre según el análisis de esta solución.

## Casos límite

- 6.a) invocado con la avenida 1 mientras el robot está parado en cualquier calle: conserva esa calle (`Pos(avenida,PosCa)`) y recorre desde ahí hasta la calle 100, no necesariamente las 99 cuadras completas si no arranca en la calle 1.
- 6.b/6.d) cuando la cadena de avenidas llega justo hasta la avenida 100 (el borde de la ciudad de 100×100), el `Pos(PosAv±k,1)` que salta a la "próxima" avenida no debe ejecutarse en la última vuelta del `repetir`, o el intérprete corta la ejecución con un error de área fuera de rango (`Pos(101,1)`/`Pos(102,1)` está fuera del área). Por eso ese salto está protegido con `si(PosAv<100)`. 6.c) no llega al borde (termina en la avenida 15), así que no necesita ese guard.
- Calcular la cantidad de vueltas del `repetir` como "diferencia entre avenida final e inicial" en vez de "diferencia más uno" deja la última avenida pedida sin recorrer — ver "Corrección aplicada" arriba para el detalle de este bug y su fix.

## Errores frecuentes

- Usar `derecha` antes de recorrer la avenida en 6.a): no hace falta, porque la orientación inicial del robot ya avanza a lo largo de las calles cuando la avenida está fija.
- Calcular la cantidad de repeticiones del `repetir` exterior en 6.b/6.c/6.d como "diferencia entre avenida final e inicial" en vez de "diferencia más uno": deja la última avenida pedida sin recorrer (era precisamente el bug corregido en esta solución).
- Al corregir ese conteo, olvidar proteger el salto final a la "próxima avenida" cuando la cadena llega hasta el borde de la ciudad (avenida 100): sin el guard `si(PosAv<100)`, el intento de `Pos` fuera del área corta la ejecución con error.

## Complejidad

Cada parte recorre O(k) avenidas de 99 pasos cada una: 6.a) es O(1) (una sola avenida); 6.b), 6.c) y 6.d) son O(k) en la cantidad de avenidas encadenadas, con un costo total de `99k` pasos.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-06-recorrer-avenidas-con-numero-parametrizado.md`](../ejercicios/ejercicio-06-recorrer-avenidas-con-numero-parametrizado.md)
- Fuente original: [`../fuentes/Capitulo 6-Parametros de Entrada.pdf`](<../fuentes/Capitulo 6-Parametros de Entrada.pdf>)
- Código: [`../codigo/soluciones/capitulo-06/Cap6_Preg_6A`](../codigo/soluciones/capitulo-06/Cap6_Preg_6A), [`../codigo/soluciones/capitulo-06/Cap6_Preg_6B`](../codigo/soluciones/capitulo-06/Cap6_Preg_6B), [`../codigo/soluciones/capitulo-06/Cap6_Preg_6C`](../codigo/soluciones/capitulo-06/Cap6_Preg_6C), [`../codigo/soluciones/capitulo-06/Cap6_Preg_6D`](../codigo/soluciones/capitulo-06/Cap6_Preg_6D)
