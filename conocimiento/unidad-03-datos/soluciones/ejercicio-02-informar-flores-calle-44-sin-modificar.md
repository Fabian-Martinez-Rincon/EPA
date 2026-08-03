---
id: "EPA-U03-EJ02-SOLUCION"
titulo: "Solución: informar la cantidad de flores de la calle 44 sin modificar las esquinas"
slug: "ejercicio-02-informar-flores-calle-44-sin-modificar"
tipo: "solucion"
unidad: 3
tema: "datos-y-variables"
subtemas:
  - "variables"
  - "tipos-de-datos"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 3-Datos.pdf"
    paginas: "1-21"
relacionados:
  - "../ejercicios/ejercicio-02-informar-flores-calle-44-sin-modificar.md"
codigo_relacionado:
  - "../codigo/capitulo-3-pregunta-02.ri"
escenario_ciudad:
  - av: 50
    ca: 44
    flores: 3
    papeles: 0
---

# Solución: informar la cantidad de flores de la calle 44 sin modificar las esquinas

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-02-informar-flores-calle-44-sin-modificar.md`](../ejercicios/ejercicio-02-informar-flores-calle-44-sin-modificar.md).

## Análisis

`Pos(1,44)` fija la calle en 44; el `derecha` orienta al robot para recorrer esa calle (avenida variable, calle fija), tal como pide el enunciado. El patrón `repetir 99 {...; mover} + chequeo final` (el mismo usado en el ejemplo 3.7 de la teoría) cubre las 100 esquinas de la calle (avenidas 1 a 100). En cada esquina se toman todas las flores contándolas en `x`, y luego se depositan de nuevo con `mientras(HayFlorEnLaBolsa) depositarFlor` antes de avanzar, de modo que la esquina queda exactamente como estaba.

## Estrategia

1. Posicionar el robot en (1,44) y girar a la derecha para orientarse a lo largo de la calle.
2. Repetir 99 veces: tomar todas las flores de la esquina actual contándolas en `x`, depositarlas de nuevo, avanzar.
3. Repetir el mismo procesamiento (sin avanzar) para la esquina final, la avenida 100.
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
    Pos(1,44)
    x:=0
    derecha
    repetir 99
      mientras(HayFlorEnLaEsquina)
        tomarFlor
        x:=x+1
      mientras (HayFlorEnLaBolsa)
        depositarFlor
      mover
    mientras(HayFlorEnLaEsquina)
      tomarFlor
      x:=x+1
    mientras(HayFlorEnLaBolsa)
      depositarFlor
    Informar(x)
  fin
variables
  robin:robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/capitulo-3-pregunta-02.ri`](../codigo/capitulo-3-pregunta-02.ri)

## Nota de alcance: sólo cubre la variante "sin modificar"

El enunciado plantea dos variantes: (1) recogiendo definitivamente las flores, o (2) sin modificar el contenido de cada esquina. El código disponible implementa únicamente la variante 2: tras contar las flores de una esquina las vuelve a depositar. La variante 1 no está implementada por separado, pero se obtiene trivialmente a partir de este mismo código quitando las dos líneas `mientras (HayFlorEnLaBolsa) depositarFlor` — no se agregó esa segunda versión para no inventar contenido no presente en el material histórico.

La variable `y` está declarada pero nunca se usa; no afecta la ejecución (se verificó con el intérprete de R-info) y se dejó tal cual porque no es un error, sólo una declaración de sobra.

## Escenario de prueba

Cargar algunas esquinas de la calle 44 con flores antes de correr la simulación (por ejemplo, 3 flores en la avenida 50) para comprobar que `x` informa el total correcto y que, al finalizar, esas esquinas conservan la misma cantidad de flores que tenían al empezar. Probado con el intérprete: con 3 flores en (50,44) y el resto de la calle vacía, informa `x = 3`.

## Casos límite

- Calle 44 completamente sin flores: `x` termina en 0, sin depositar nada.
- Una esquina con varias flores: se toman y se depositan todas juntas, sin perder la cuenta.

## Errores frecuentes

- Olvidarse de volver a depositar las flores tomadas, lo que convertiría esta solución en la variante 1 (recogiendo) en vez de la 2 (sin modificar).
- Confundir avenida y calle al invocar `Pos`, dejando fija la avenida en lugar de la calle.

## Complejidad

Recorrido fijo de 100 esquinas (una calle completa): O(1) respecto al tamaño de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-02-informar-flores-calle-44-sin-modificar.md`](../ejercicios/ejercicio-02-informar-flores-calle-44-sin-modificar.md)
- Fuente original: [`../fuentes/Capitulo 3-Datos.pdf`](<../fuentes/Capitulo 3-Datos.pdf>)
- Código: [`../codigo/capitulo-3-pregunta-02.ri`](../codigo/capitulo-3-pregunta-02.ri)
