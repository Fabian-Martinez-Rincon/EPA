---
id: "EPA-U07-EJ06-SOLUCION"
titulo: "Solución: recorrer cuadrados decrecientes hasta hallar 3 flores y 2 papeles"
slug: "ejercicio-06-cuadrados-decrecientes-3-flores-2-papeles"
tipo: "solucion"
unidad: 7
tema: "parametros-de-entrada-salida"
subtemas:
  - "parametro-e-y-es-combinados"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 7-Parametros de Entrada-Salida.pdf"
    paginas: "10"
relacionados:
  - "../ejercicios/ejercicio-06-cuadrados-decrecientes-3-flores-2-papeles.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-07/Cap7_Preg_6"
escenario_ciudad:
  - av: 1
    ca: 1
    flores: 3
  - av: 1
    ca: 2
    papeles: 2
---

# Solución: recorrer cuadrados decrecientes hasta hallar 3 flores y 2 papeles

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-06-cuadrados-decrecientes-3-flores-2-papeles.md`](../ejercicios/ejercicio-06-cuadrados-decrecientes-3-flores-2-papeles.md).

## Análisis

El proceso `cuadrado` combina los dos modos de parámetro: `Lado` es de entrada (`E`, cada cuadrado tiene un tamaño distinto que solo entra al proceso) y `FLORES`/`PAPELES` son de entrada/salida (`ES`, acumulan lo hallado en el recorrido de ese cuadrado y lo devuelven al llamador). Recorre el perímetro (`repetir 4` lados de `Lado` esquinas cada uno, con un `derecha` en cada vértice) tomando y depositando de nuevo cada flor/papel que encuentra — el patrón "sin modificar" ya visto en el Ejemplo 7.1, aplicado esquina por esquina en vez de a toda una avenida.

Todos los cuadrados comparten el vértice (1,1) como esquina de partida (el programa nunca reposiciona al robot entre un cuadrado y el siguiente, y cada `cuadrado` termina exactamente donde empezó tras las 4 vueltas de `derecha`), así que "decrementar el lado" no arma cuadrados concéntricos sino cuadrados anidados desde la misma esquina — el enunciado no exige una disposición concreta, solo que el primer lado sea 99 y cada uno decrezca en 1.

## Corrección aplicada durante esta organización

El archivo histórico tenía dos problemas puntuales, corregidos en esta organización:

1. **`lado:=14` en vez de `lado:=99`.** El enunciado fija explícitamente "el primer cuadrado es de lado 99"; el archivo arrancaba en 14 (muy probablemente un valor de prueba que quedó sin revertir). Se corrigió a `lado:=99`.
2. **`mientras(~(flores=3)&~(papeles=2))` en vez de `mientras(~(flores=3)|~(papeles=2))`.** La condición de corte tiene que seguir buscando mientras **no** se cumplan **ambas** condiciones a la vez (3 flores Y 2 papeles); por De Morgan, la negación correcta de "ambas" (`&`) es "cualquiera de las dos falla" (`|`), no "las dos fallan" (`&`). Con el `&` original, el recorrido se detenía apenas un cuadrado tenía 3 flores (sin importar cuántos papeles) o apenas tenía 2 papeles (sin importar cuántas flores), devolviendo un cuadrado que no cumple lo pedido. Se verificó la diferencia con un programa mínimo contra el intérprete de R-info: con `flores=3` y `papeles=5` de partida, la versión con `&` no entra ni una vez al `mientras` (deja `papeles` en 5, mal), mientras que la versión con `|` entra una vez, corrige `papeles` a 2 y recién ahí se detiene.

## Estrategia

1. Empezar con lado 99 en la esquina (1,1).
2. Mientras no se haya encontrado un cuadrado con exactamente 3 flores y 2 papeles: reiniciar los acumuladores, recorrer el perímetro del cuadrado actual (sin modificar su contenido), informar el lado y lo hallado en el cuadrado recién recorrido, y recién después decrementar el lado en 1.

## Código relacionado

```rinfo
programa Captitulo7Pregunta6
procesos
  proceso cuadrado(E Lado:numero;ES FLORES:numero;ES PAPELES:numero)
  variables
    CantPapeles:numero
    CantFlores:numero
  comenzar
    repetir 4
      repetir Lado
        CantFlores:=0
        CantPapeles:=0
        mientras(HayFlorEnLaEsquina)|(HayPapelEnLaEsquina)
          si(HayFlorEnLaEsquina)
            tomarFlor
            FLORES:=FLORES+1
            CantFlores:=CantFlores+1
          si(HayPapelEnLaEsquina)
            tomarPapel
            PAPELES:=PAPELES+1
            CantPapeles:=CantPapeles+1
        repetir CantFlores
          depositarFlor
        repetir CantPapeles
          depositarPapel
        mover
      derecha
  fin
areas
  ciudad:AreaC(1,1,100,100)
robots
  robot robot1
  variables
    lado,flores:numero
    papeles:numero
    menos:numero
  comenzar
    menos:=-1
    lado:=99
    mientras(~(flores=3)|~(papeles=2))
      flores:=0
      papeles:=0
      cuadrado(lado,flores,papeles)
      Informar(lado,flores,papeles)
      lado:=lado+menos
  fin
variables
  R-Info: robot1
comenzar
  AsignarArea(R-Info,ciudad)
  Iniciar(R-Info,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-07/Cap7_Preg_6`](../codigo/soluciones/capitulo-07/Cap7_Preg_6)

## Escenario de prueba

El escenario siembra 3 flores en (1,1) y 2 papeles en (1,2). Las dos esquinas caen sobre el primer lado del cuadrado de lado 99, así que el primer cuadrado que el robot recorre ya cumple la condición: un solo `Informar`, con los valores 99, 3 y 2.

El `Informar` va antes del `lado:=lado+menos`, así que el número que sale es el lado del cuadrado que el robot acaba de recorrer.

## Casos límite

- Si ningún cuadrado cumple, el programa no termina nunca. Cuando `lado` llega a 0 y sigue bajando, `repetir Lado` no ejecuta ninguna vuelta: el robot se queda quieto, `flores` y `papeles` vuelven a 0 y el `mientras` se repite para siempre.
- Un cuadrado con 3 flores pero un solo papel no sirve. Las dos cuentas tienen que dar justo, y el robot pasa al cuadrado siguiente.

## Errores frecuentes

- Negar la condición con `&` en vez de `|`. Hay que seguir buscando mientras falle **cualquiera** de las dos cuentas. Con `&` el robot frena en el primer cuadrado que tenga 3 flores sin mirar los papeles: con 3 flores y 5 papeles informa 99, 3 y 5, y da la búsqueda por terminada.
- Arrancar con un lado de prueba en vez de 99, que es el que fija el enunciado.
- Decrementar el lado antes del `Informar`. El número que sale es el del cuadrado siguiente: para el de lado 99 informa 98.
- No reiniciar `flores` y `papeles` antes de cada cuadrado. Son parámetros `ES`: entran con el valor que traen, así que el cuadrado siguiente contaría además todo lo del anterior.

## Complejidad

Cada cuadrado de lado L se recorre en O(L) (4×L esquinas). En el peor caso se recorren los 99 cuadrados (lados 99 a 1), es decir O(99²) esquinas visitadas en total — O(1) respecto al tamaño fijo de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-06-cuadrados-decrecientes-3-flores-2-papeles.md`](../ejercicios/ejercicio-06-cuadrados-decrecientes-3-flores-2-papeles.md)
- Código: [`../codigo/soluciones/capitulo-07/Cap7_Preg_6`](../codigo/soluciones/capitulo-07/Cap7_Preg_6)
