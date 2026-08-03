---
id: "EPA-U07-EJ05-SOLUCION"
titulo: "Solución: pasos hasta encontrar flor o papel en cada calle impar"
slug: "ejercicio-05-pasos-hasta-flor-o-papel-calles-impares"
tipo: "solucion"
unidad: 7
tema: "parametros-de-entrada-salida"
subtemas:
  - "parametro-es-como-salida"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 7-Parametros de Entrada-Salida.pdf"
    paginas: "10"
relacionados:
  - "../ejercicios/ejercicio-05-pasos-hasta-flor-o-papel-calles-impares.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-07/Cap7_Preg_5"
escenario_ciudad:
  - av: 5
    ca: 1
    flores: 1
  - av: 5
    ca: 3
    papeles: 1
  - av: 5
    ca: 5
    flores: 1
  - av: 5
    ca: 7
    papeles: 1
  - av: 5
    ca: 9
    flores: 1
  - av: 5
    ca: 11
    papeles: 1
  - av: 5
    ca: 13
    flores: 1
  - av: 5
    ca: 15
    papeles: 1
  - av: 5
    ca: 17
    flores: 1
  - av: 5
    ca: 19
    papeles: 1
  - av: 5
    ca: 21
    flores: 1
  - av: 5
    ca: 23
    papeles: 1
  - av: 5
    ca: 25
    flores: 1
  - av: 5
    ca: 27
    papeles: 1
  - av: 5
    ca: 29
    flores: 1
  - av: 5
    ca: 31
    papeles: 1
  - av: 5
    ca: 33
    flores: 1
  - av: 5
    ca: 35
    papeles: 1
  - av: 5
    ca: 37
    flores: 1
  - av: 5
    ca: 39
    papeles: 1
  - av: 5
    ca: 41
    flores: 1
  - av: 5
    ca: 43
    papeles: 1
  - av: 5
    ca: 45
    flores: 1
  - av: 5
    ca: 47
    papeles: 1
  - av: 5
    ca: 49
    flores: 1
  - av: 5
    ca: 51
    papeles: 1
  - av: 5
    ca: 53
    flores: 1
  - av: 5
    ca: 55
    papeles: 1
  - av: 5
    ca: 57
    flores: 1
  - av: 5
    ca: 59
    papeles: 1
  - av: 5
    ca: 61
    flores: 1
  - av: 5
    ca: 63
    papeles: 1
  - av: 5
    ca: 65
    flores: 1
  - av: 5
    ca: 67
    papeles: 1
  - av: 5
    ca: 69
    flores: 1
  - av: 5
    ca: 71
    papeles: 1
  - av: 5
    ca: 73
    flores: 1
  - av: 5
    ca: 75
    papeles: 1
  - av: 5
    ca: 77
    flores: 1
  - av: 5
    ca: 79
    papeles: 1
  - av: 5
    ca: 81
    flores: 1
  - av: 5
    ca: 83
    papeles: 1
  - av: 5
    ca: 85
    flores: 1
  - av: 5
    ca: 87
    papeles: 1
  - av: 5
    ca: 89
    flores: 1
  - av: 5
    ca: 91
    papeles: 1
  - av: 5
    ca: 93
    flores: 1
  - av: 5
    ca: 95
    papeles: 1
  - av: 5
    ca: 97
    flores: 1
  - av: 5
    ca: 99
    papeles: 1
---

# Solución: pasos hasta encontrar flor o papel en cada calle impar

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-05-pasos-hasta-flor-o-papel-calles-impares.md`](../ejercicios/ejercicio-05-pasos-hasta-flor-o-papel-calles-impares.md).

## Análisis

El proceso `CallesImpares` recibe `contar` como parámetro de entrada/salida usado únicamente como salida (patrón de la sección 7.3 del capítulo: el proceso no necesita el valor de entrada, solo lo usa para devolver un resultado calculado internamente). Cada llamada es autocontenida en cuanto a orientación: entra con la orientación por defecto (`mover` incrementa `PosCa`), hace un `derecha` para quedar orientado a lo largo de la calle (`mover` incrementa `PosAv`, calle fija — "recorre una calle" según la regla de orientación del robot), recorre hasta encontrar flor o papel, informa, y antes de salir hace `izquierda` (tres `derecha`), con lo que la orientación neta dentro de la llamada es `derecha` + `izquierda` = 4 giros = 360°, volviendo exactamente a la orientación por defecto para la siguiente llamada. Por eso el llamador (`repetir 50: contador:=0; CallesImpares(contador)`) puede invocar el proceso repetidamente sin preocuparse por la orientación acumulada.

La condición de corte `mientras(~(HayFlorEnLaEsquina))&(~(HayPapelEnLaEsquina))` es la negación correcta (por De Morgan) de "hay flor o papel": el recorrido continúa exactamente mientras NO hay flor Y NO hay papel, y se detiene en cuanto aparece cualquiera de los dos.

## Estrategia

1. Por cada una de las 50 calles impares (1, 3, 5, …, 99): reiniciar el contador de pasos en 0 e invocar `CallesImpares`.
2. Dentro de `CallesImpares`: orientarse a lo largo de la calle, avanzar contando pasos mientras la esquina actual no tenga ni flor ni papel, informar el conteo al encontrar la esquina buscada, y reposicionarse al inicio de la siguiente calle impar (saltando la par intermedia) — excepto si la calle recién procesada es la 99 (la última), caso en el que no hay una calle impar siguiente a la cual saltar.

## Corrección aplicada durante esta organización

El archivo histórico tenía dos problemas encadenados relacionados con la cantidad de calles impares (50, no 99), ambos verificados con el intérprete de R-info de Academia-Fabo:

1. **`repetir 99` en vez de `repetir 50` en el programa principal.** Solo hay 50 calles impares entre 1 y 100 (1, 3, 5, …, 99); el `repetir 99` original invocaba a `CallesImpares` 49 veces de más.
2. **`Pos(1,PosCa+2)` incondicional dentro de `CallesImpares`.** Al terminar de procesar la calle 99 (la última impar), el proceso igual intentaba reposicionarse a la "siguiente calle impar" (la 101), inexistente en `AreaC(1,1,100,100)`. Antes de esta corrección esto cortaba la ejecución con el error `Pos(1,101) está fuera del área`, y ocurría en la llamada número 50 — es decir, con solo cambiar `repetir 99` por `repetir 50` el corte seguía sucediendo igual, porque el problema no era la cantidad de invocaciones sino que el proceso nunca comprobaba si quedaba una calle impar siguiente antes de saltar. Se agregó el chequeo `si(PosCa<99) Pos(1,PosCa+2)` (mismo patrón que el caso análogo en [`../../unidad-02-algoritmos-y-logica/soluciones/ejercicio-12-esquina-libre-depositar-papel.md`](../../unidad-02-algoritmos-y-logica/soluciones/ejercicio-12-esquina-libre-depositar-papel.md)).

Se verificaron ambos cambios juntos contra el intérprete, con tres escenarios:

- El escenario real del front matter (flor/papel siempre en avenida 5 de cada calle impar): las 50 llamadas informan `4` pasos cada una y el programa termina limpio (evento `fin`), sin ningún evento de error.
- Flor/papel siempre en avenida 1 de cada calle impar (caso límite de 0 pasos): las 50 llamadas informan `0` cada una, también sin error.
- Flor/papel a distancia creciente por calle (avenida 1, 2, 3, …, 50 según la calle): se informan exactamente los valores `0, 1, 2, …, 49` en orden, confirmando que el conteo de pasos es correcto en todo el rango, no solo en el caso constante del front matter.

En los tres casos el programa produce exactamente 50 `Informar`, uno por calle impar, y termina sin errores — el comportamiento que pide el enunciado.

## Código relacionado

```
programa Capitulo7Pregunta5
procesos
  proceso izquierda
  comenzar
    repetir 3
      derecha
  fin
  proceso CallesImpares(ES contar:numero)
  comenzar
    derecha
    mientras(~(HayFlorEnLaEsquina))&(~(HayPapelEnLaEsquina))
      mover
      contar:=contar+1
    Informar(contar)
    si(PosCa<99)
      Pos(1,PosCa+2)
    izquierda
  fin
areas
  ciudad:AreaC(1,1,100,100)
robots
  robot robot1
  variables
    contador:numero
  comenzar
    repetir 50
      contador:=0
      CallesImpares(contador)
  fin
variables
  R-Info:robot1
comenzar
  AsignarArea(R-Info,ciudad)
  Iniciar(R-Info,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-07/Cap7_Preg_5`](../codigo/soluciones/capitulo-07/Cap7_Preg_5)

## Escenario de prueba

El escenario del front matter siembra una flor o un papel en cada una de las 50 calles impares, siempre en la avenida 5 — se observan las 50 llamadas informando 4 pasos cada una y el robot termina el recorrido sin salirse del área.

## Casos límite

- Flor o papel exactamente en la avenida 1 de una calle impar: el `mientras` no ejecuta ninguna vuelta (la condición ya es falsa en la primera esquina), se informa 0 pasos. Verificado contra el intérprete.
- Calle impar sin flor ni papel (violación de la garantía del enunciado): el robot llega hasta la avenida 100 y el siguiente `mover` falla por salirse de la ciudad.
- Calle 99 (la última impar procesada): se informa correctamente su conteo de pasos y, gracias al chequeo `si(PosCa<99)`, no se intenta reposicionar a la calle 101 — el programa termina limpio después de esa última llamada.

## Errores frecuentes

- Escribir la condición de corte con `|` en vez de `&` (o sin negar ambos términos), lo que detendría el recorrido en la esquina equivocada.
- Asumir que "recorrer todas las calles impares" necesita `repetir 99` en vez de `repetir 50` — uno de los dos bugs reales que tenía este archivo, corregido arriba.
- Reposicionar incondicionalmente a la siguiente calle impar sin comprobar si es la última — el otro bug real de este archivo: aunque se corrija la cantidad de repeticiones del llamador, el `Pos` sin guardia sigue intentando saltar a la calle 101 al terminar la calle 99.
- Olvidar el `izquierda` final dentro de `CallesImpares`, lo que dejaría al robot mal orientado para la llamada siguiente.

## Complejidad

Cada calle impar se recorre en O(distancia hasta la primera esquina con flor o papel), acotado por O(100). Para las 50 calles impares, el total es O(50×100) en el peor caso, es decir O(1) respecto al tamaño fijo de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-05-pasos-hasta-flor-o-papel-calles-impares.md`](../ejercicios/ejercicio-05-pasos-hasta-flor-o-papel-calles-impares.md)
- Fuente original: [`../fuentes/Capitulo 7-Parametros de Entrada-Salida.pdf`](<../fuentes/Capitulo 7-Parametros de Entrada-Salida.pdf>)
- Código: [`../codigo/soluciones/capitulo-07/Cap7_Preg_5`](../codigo/soluciones/capitulo-07/Cap7_Preg_5)
