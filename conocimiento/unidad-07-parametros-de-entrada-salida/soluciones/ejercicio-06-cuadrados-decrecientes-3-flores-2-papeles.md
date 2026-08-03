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
2. Mientras no se haya encontrado un cuadrado con exactamente 3 flores y 2 papeles: reiniciar los acumuladores, recorrer el perímetro del cuadrado actual (sin modificar su contenido), decrementar el lado en 1 e informar el resultado del cuadrado recién recorrido.

## Código relacionado

```
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
      lado:=lado+menos
      Informar(lado,flores,papeles)
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

Probado contra el intérprete de R-info de Academia-Fabo sembrando la ciudad con 3 flores en (1,1) y 2 papeles en (1,2) — ambas esquinas caen dentro del primer lado de cualquier cuadrado anclado en (1,1), así que el cuadrado de lado 99 ya cumple la condición: el programa termina en la primera vuelta del `mientras`, informando `(98, 3, 2)` (el lado ya decrementado en 1 en el momento de informar). Sin flores/papeles sembrados, el primer cuadrado tiene (0,0) y el recorrido sigue decreciendo el lado normalmente.

## Casos límite

- El cuadrado buscado es el primero (lado 99): se informa una sola vez.
- `lado` llega a 0 o negativo (si ningún cuadrado entre 99 y 1 cumple la condición, lo que contradice la garantía del enunciado): `repetir Lado` con `Lado<=0` no ejecuta ninguna vuelta, así que el robot se queda quieto y `flores`/`papeles` quedan en 0 indefinidamente — el `mientras` no terminaría nunca en ese escenario (no puede ocurrir si se respeta la garantía del enunciado).
- Cuadrado con 3 flores pero no 2 papeles (o viceversa): con la corrección aplicada, el recorrido sigue buscando; con el bug original, se detenía ahí incorrectamente (ver "Corrección aplicada" arriba).

## Errores frecuentes

- Usar `&` en lugar de `|` al negar una condición conjunta (bug real de este archivo, corregido arriba) — un error clásico de aplicar De Morgan al revés.
- Dejar un valor de prueba (`lado:=14`) en el código en vez del valor que pide el enunciado (99) — el otro bug real de este archivo.
- Olvidar reiniciar `FLORES`/`PAPELES` en el llamador antes de cada cuadrado, lo que acumularía de más entre cuadrados sucesivos.

## Complejidad

Cada cuadrado de lado L se recorre en O(L) (4×L esquinas). En el peor caso se recorren los 99 cuadrados (lados 99 a 1), es decir O(99²) esquinas visitadas en total — O(1) respecto al tamaño fijo de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-06-cuadrados-decrecientes-3-flores-2-papeles.md`](../ejercicios/ejercicio-06-cuadrados-decrecientes-3-flores-2-papeles.md)
- Fuente original: [`../fuentes/Capitulo 7-Parametros de Entrada-Salida.pdf`](<../fuentes/Capitulo 7-Parametros de Entrada-Salida.pdf>)
- Código: [`../codigo/soluciones/capitulo-07/Cap7_Preg_6`](../codigo/soluciones/capitulo-07/Cap7_Preg_6)
