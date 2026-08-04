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
estado: "completo"
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
2. Repetir 99 veces (una por calle, calles 1 a 99): repetir 99 veces (avanzando por la calle) chequear si la esquina está vacía y avanzar; chequear la última avenida de esa calle; saltar al comienzo de la siguiente calle con `Pos(1,PosCa+1)`.
3. Procesar la calle 100 con el mismo patrón (repetir 99 chequeo+avance, más el chequeo de la última avenida), ya que el `Pos(1,PosCa+1)` de la última vuelta del paso 2 deja al robot posicionado en (1,100), el comienzo de esa calle.
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
    repetir 99
      si ~((HayFlorEnLaEsquina)|(HayPapelEnLaEsquina))
        x:=x+1
      mover
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

## Correcciones aplicadas durante esta organización

Se aplicaron dos correcciones, ambas verificadas con el intérprete de R-info:

1. **Operador `|` faltante (impedía parsear el archivo):** la condición que chequea la última avenida de cada calle (dentro del `repetir 99` exterior, justo después del `repetir 99` interior) estaba escrita como `si~((HayFlorEnLaEsquina)(HayPapelEnLaEsquina))`, sin ningún operador entre los dos paréntesis — el intérprete rechazaba esto directamente con un error de parseo ("Se esperaba \")\" y se encontró \"(\" en la línea 19"). Las otras dos apariciones de la misma condición en el mismo archivo (dentro del `repetir` interior y en el chequeo final) sí usan `|` correctamente, así que se agregó el `|` faltante para que las tres condiciones queden idénticas.
2. **Calle 100 sin recorrer (bug de alcance, corregido en esta pasada):** aun con el `|` corregido, el archivo dejaba sin revisar 99 de las 100 esquinas de la última calle. El `repetir 99` exterior completa las calles 1 a 99 y termina posicionando al robot en (1,100) — el comienzo de la calle 100 — pero después de ese `repetir` sólo había **un** chequeo suelto (para la esquina (1,100)), sin recorrer el resto de la calle. Verificado con el intérprete sobre una ciudad vacía: el archivo (con sólo el fix del `|`) informaba **9901** en vez de 10000, una diferencia de exactamente 99 (el tamaño de la calle 100 menos la única esquina chequeada). Se corrigió agregando, después del `repetir` exterior, el mismo bloque `repetir 99 {chequeo; mover}` + chequeo final que ya usa cada calle dentro del bucle — un bloque duplicado, sin lógica nueva. Con la corrección, el mismo escenario (ciudad vacía) informa `x = 10000`; el escenario real del front matter (3 esquinas ocupadas) informa `x = 9997` (10000 − 3); y una esquina ocupada específicamente en la calle 100 (por ejemplo (55,100)) ahora se descuenta correctamente (`x = 9999` sobre ciudad vacía con esa única esquina ocupada), confirmando que la calle 100 ya se revisa por completo.

## Escenario de prueba

Conviene iniciar la simulación con la ciudad casi vacía salvo algunas esquinas sueltas con flor o papel, para comprobar que `x` cuenta correctamente las esquinas vacías de toda la ciudad, incluida la calle 100. Probado con el intérprete: con el escenario del front matter (flor en (10,10), papel en (50,50), flor+papel en (90,20)), informa `x = 9997`.

## Casos límite

- Ciudad completamente vacía: `x` informa 10000.
- Esquina con flor pero sin papel, o viceversa: no cuenta como vacía (la condición exige ausencia de ambos).
- Esquina ocupada en la calle 100 (la última en recorrerse): se descuenta correctamente, confirmando que esa calle ya no queda fuera del recorrido.

## Errores frecuentes

- Olvidar el operador entre dos proposiciones atómicas al escribir una conjunción o disyunción negada (el primer bug real que tenía este archivo).
- Asumir que el `Pos(1,PosCa+1)` al final de cada calle implica que la última calle también se recorre por completo — el segundo bug real que tenía este archivo; hace falta un bloque de recorrido explícito después del `repetir` exterior para cubrir esa última calle.

## Complejidad

Recorrido completo de las 10000 esquinas de la ciudad: O(n²) en el tamaño de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-03-informar-esquinas-vacias-ciudad.md`](../ejercicios/ejercicio-03-informar-esquinas-vacias-ciudad.md)
- Código: [`../codigo/capitulo-3-pregunta-03.ri`](../codigo/capitulo-3-pregunta-03.ri)
