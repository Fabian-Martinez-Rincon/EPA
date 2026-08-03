---
id: "EPA-U03-EJ03-SOLUCION"
titulo: "Solución: informar la cantidad de esquinas vacías de la ciudad"
slug: "ejercicio-03-informar-esquinas-vacias-ciudad"
tipo: "solucion"
unidad: 3
tema: "datos-y-variables"
subtemas:
  - "variables"
  - "estructuras-de-control"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "parcial"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 3-Datos.pdf"
    paginas: "1-21"
relacionados:
  - "../ejercicios/ejercicio-03-informar-esquinas-vacias-ciudad.md"
codigo_relacionado:
  - "../codigo/capitulo-3-pregunta-03.ri"
escenario_ciudad:
  - av: 10
    ca: 10
    flores: 1
    papeles: 0
  - av: 50
    ca: 50
    flores: 0
    papeles: 1
  - av: 90
    ca: 20
    flores: 1
    papeles: 1
---

# Solución: informar la cantidad de esquinas vacías de la ciudad

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-03-informar-esquinas-vacias-ciudad.md`](../ejercicios/ejercicio-03-informar-esquinas-vacias-ciudad.md).

## Análisis

Para cubrir las 10000 esquinas de la ciudad se anida un `repetir 99` (una vez por calle) dentro de otro `repetir 99` (avanzando por las avenidas de esa calle), con un chequeo de la última avenida de cada calle y un `Pos(1,PosCa+1)` para saltar al comienzo de la siguiente. Al final del `repetir` exterior se chequea una última esquina.

## Estrategia

1. Girar a la derecha para orientarse a lo largo de una calle (avenida variable).
2. Repetir 99 veces (una por calle): repetir 99 veces (avanzando por la calle) chequear si la esquina está vacía y avanzar; chequear la última avenida de esa calle; saltar al comienzo de la siguiente calle con `Pos(1,PosCa+1)`.
3. Chequear una esquina final.
4. Informar `x`.

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
    x:=0
    derecha
    repetir 99
      repetir 99
        si ~((HayFlorEnLaEsquina)|(HayPapelEnLaEsquina))
          x:=x+1
        mover
      si~((HayFlorEnLaEsquina)|(HayPapelEnLaEsquina))
        x:=x+1
      Pos(1,PosCa+1)
    si~((HayFlorEnLaEsquina)|(HayPapelEnLaEsquina))
      x:=x+1
    Informar(x)
  fin
variables
  robin:robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/capitulo-3-pregunta-03.ri`](../codigo/capitulo-3-pregunta-03.ri)

## Corrección aplicada durante esta organización

La condición que chequea la última avenida de cada calle (dentro del `repetir 99` exterior, justo después del `repetir 99` interior) estaba escrita como `si~((HayFlorEnLaEsquina)(HayPapelEnLaEsquina))`, sin ningún operador entre los dos paréntesis — el intérprete de R-info rechaza esto directamente con un error de parseo ("Se esperaba \")\" y se encontró \"(\" en la línea 19"). Las otras dos apariciones de la misma condición en el mismo archivo (dentro del `repetir` interior y en el chequeo final) sí usan `|` correctamente, así que se agregó el `|` faltante para que las tres condiciones queden idénticas, como sin duda se pretendía.

## Alcance no corregido: la calle 100 no se recorre completa

Aun con el `|` corregido, el patrón de este archivo deja sin revisar 99 de las 100 esquinas de la última calle. El `repetir 99` exterior completa las calles 1 a 99 (cada una con sus 100 esquinas, gracias al `repetir 99` interior + el chequeo de la avenida 100 + el salto `Pos(1,PosCa+1)`), y termina posicionando al robot en (1,100) — el comienzo de la calle 100. Pero después del `repetir` exterior sólo hay **un** chequeo suelto (para la esquina (1,100)), no un recorrido completo de esa calle: las esquinas (2,100) a (100,100) nunca se visitan.

Se verificó esto ejecutando el archivo corregido con el intérprete de R-info sobre una ciudad completamente vacía: en vez de informar 10000 (las 10000 esquinas vacías), informa **9901** (9900 de las calles 1 a 99, más 1 sola esquina de la calle 100) — una diferencia de exactamente 99, que es justamente el tamaño de la calle 100 menos la única esquina que sí se chequea. Arreglar esto requeriría agregar, después del `repetir` exterior, una repetición completa (un `repetir 99 {chequeo; mover}` más un chequeo final) igual a la que ya usa cada calle dentro del bucle — es decir, duplicar un bloque de estructura entero, no ajustar una palabra o un operador. Por eso se deja documentado en vez de reescrito, siguiendo el mismo criterio que en `ejercicio-12` de la unidad 2.

## Escenario de prueba

Conviene iniciar la simulación con la ciudad casi vacía salvo algunas esquinas sueltas con flor o papel, para comprobar que `x` cuenta correctamente las esquinas vacías de las calles 1 a 99. Tener en cuenta la limitación de la calle 100 explicada arriba al interpretar el resultado si se puebla esa calle específicamente.

## Casos límite

- Ciudad completamente vacía: `x` informa 9901, no 10000 (ver nota de alcance).
- Esquina con flor pero sin papel, o viceversa: no cuenta como vacía (la condición exige ausencia de ambos).

## Errores frecuentes

- Olvidar el operador entre dos proposiciones atómicas al escribir una conjunción o disyunción negada (el bug real que tenía este archivo).
- Asumir que el `Pos(1,PosCa+1)` al final de cada calle implica que la última calle también se recorre por completo — como se explica arriba, no es así en este archivo.

## Complejidad

Recorrido de hasta 9901 esquinas efectivamente chequeadas (no las 10000 de la ciudad completa, ver nota de alcance): O(n²) en el tamaño de la ciudad, con el límite superior fijo de este código.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-03-informar-esquinas-vacias-ciudad.md`](../ejercicios/ejercicio-03-informar-esquinas-vacias-ciudad.md)
- Fuente original: [`../fuentes/Capitulo 3-Datos.pdf`](<../fuentes/Capitulo 3-Datos.pdf>)
- Código: [`../codigo/capitulo-3-pregunta-03.ri`](../codigo/capitulo-3-pregunta-03.ri)
