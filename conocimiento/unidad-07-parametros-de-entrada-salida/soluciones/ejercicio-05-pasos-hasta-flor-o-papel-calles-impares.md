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
estado: "parcial"
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

El proceso `CallesImpares` recibe `contar` como parámetro de entrada/salida usado únicamente como salida (patrón de la sección 7.3 del capítulo: el proceso no necesita el valor de entrada, solo lo usa para devolver un resultado calculado internamente). Cada llamada es autocontenida en cuanto a orientación: entra con la orientación por defecto (`mover` incrementa `PosCa`), hace un `derecha` para quedar orientado a lo largo de la calle (`mover` incrementa `PosAv`, calle fija — "recorre una calle" según la regla de orientación del robot), recorre hasta encontrar flor o papel, informa, y antes de salir hace `izquierda` (tres `derecha`), con lo que la orientación neta dentro de la llamada es `derecha` + `izquierda` = 4 giros = 360°, volviendo exactamente a la orientación por defecto para la siguiente llamada. Por eso el llamador (`repetir 99: contador:=0; CallesImpares(contador)`) puede invocar el proceso repetidamente sin preocuparse por la orientación acumulada.

La condición de corte `mientras(~(HayFlorEnLaEsquina))&(~(HayPapelEnLaEsquina))` es la negación correcta (por De Morgan) de "hay flor o papel": el recorrido continúa exactamente mientras NO hay flor Y NO hay papel, y se detiene en cuanto aparece cualquiera de los dos.

## Estrategia

1. Por cada una de las 50 calles impares (1, 3, 5, …, 99): reiniciar el contador de pasos en 0 e invocar `CallesImpares`.
2. Dentro de `CallesImpares`: orientarse a lo largo de la calle, avanzar contando pasos mientras la esquina actual no tenga ni flor ni papel, informar el conteo al encontrar la esquina buscada, y reposicionarse al inicio de la siguiente calle impar (saltando la par intermedia).

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
    repetir 99
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

## Alcance no corregido: intenta procesar más calles impares de las que existen

El `repetir 99` del programa principal asume, por copia del patrón habitual "recorrer todo con 99 repeticiones", que hay 99 calles para procesar — pero solo hay 50 calles impares entre 1 y 100 (1, 3, 5, …, 99). Probando este archivo contra el intérprete de R-info construido para Academia-Fabo (sembrando una flor en cada una de las 50 calles impares para que el recorrido siempre encuentre algo) se confirmó que las 50 llamadas válidas ocurren correctamente, cada una informando su conteo de pasos — pero, al llegar a la calle 99 (la última impar), `CallesImpares` ejecuta incondicionalmente `Pos(1,PosCa+2)` para saltar a la "siguiente calle impar", que sería la 101: inexistente en una ciudad `AreaC(1,1,100,100)`. El intérprete corta la ejecución con el error `Pos(1,101) está fuera del área`.

No se corrigió porque no es un fix de una palabra suelta: acotar el `repetir 99` del llamador a `repetir 50` **no alcanza**, porque el `Pos(1,PosCa+2)` que falla está dentro de `CallesImpares` y se ejecuta sin condición en cada invocación, incluida la que procesa la calle 99 (la última válida) — el problema no es "se invoca de más", sino que el proceso nunca verifica si todavía queda una calle impar siguiente antes de saltar. Arreglarlo de verdad requiere agregar una condición nueva (al estilo `si(PosCa<99) Pos(1,PosCa+2)`, mismo patrón que el caso análogo documentado en [`../../unidad-02-algoritmos-y-logica/soluciones/ejercicio-12-esquina-libre-depositar-papel.md`](../../unidad-02-algoritmos-y-logica/soluciones/ejercicio-12-esquina-libre-depositar-papel.md)), lo cual es un cambio de estructura, no una corrección quirúrgica.

Importante: este corte ocurre **después** de que las 50 esquinas buscadas ya fueron encontradas e informadas correctamente — el resultado observable que pide el enunciado (un `Informar` por cada calle impar) se entrega en su totalidad antes del error final.

## Escenario de prueba

Para poder observar las 50 esquinas encontradas conviene que la simulación arranque con al menos una flor o un papel en cada calle impar (si alguna calle impar no tuviera nada, el recorrido de esa calle llegaría hasta la avenida 100 y de ahí en más el `mover` fallaría por salirse de la ciudad, antes incluso de llegar al error de reposicionamiento entre calles).

## Casos límite

- Flor o papel exactamente en la avenida 1 de una calle impar: el `mientras` no ejecuta ninguna vuelta (la condición ya es falsa en la primera esquina), se informa 0 pasos.
- Calle impar sin flor ni papel (violación de la garantía del enunciado): el robot llega hasta la avenida 100 y el siguiente `mover` falla por salirse de la ciudad, distinto del error de reposicionamiento entre calles descrito arriba.
- Calle 99 (la última impar procesada): se informa correctamente su conteo de pasos, y solo después de informarlo se produce el corte de ejecución al intentar reposicionarse a la calle 101 (ver más arriba).

## Errores frecuentes

- Escribir la condición de corte con `|` en vez de `&` (o sin negar ambos términos), lo que detendría el recorrido en la esquina equivocada.
- Asumir que "recorrer todas las calles impares" necesita `repetir 99` en vez de `repetir 50` — el bug real que tiene este archivo, documentado arriba sin corregir por ser un problema de alcance, no de una palabra.
- Olvidar el `izquierda` final dentro de `CallesImpares`, lo que dejaría al robot mal orientado para la llamada siguiente.

## Complejidad

Cada calle impar se recorre en O(distancia hasta la primera esquina con flor o papel), acotado por O(100). Para las 50 calles impares, el total es O(50×100) en el peor caso, es decir O(1) respecto al tamaño fijo de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-05-pasos-hasta-flor-o-papel-calles-impares.md`](../ejercicios/ejercicio-05-pasos-hasta-flor-o-papel-calles-impares.md)
- Fuente original: [`../fuentes/Capitulo 7-Parametros de Entrada-Salida.pdf`](<../fuentes/Capitulo 7-Parametros de Entrada-Salida.pdf>)
- Código: [`../codigo/soluciones/capitulo-07/Cap7_Preg_5`](../codigo/soluciones/capitulo-07/Cap7_Preg_5)
