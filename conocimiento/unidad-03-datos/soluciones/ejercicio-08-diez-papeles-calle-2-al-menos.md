---
id: "EPA-U03-EJ08-SOLUCION"
titulo: "Solución: caminar la calle 2 hasta encontrar al menos 10 papeles"
slug: "ejercicio-08-diez-papeles-calle-2-al-menos"
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
  - "../ejercicios/ejercicio-08-diez-papeles-calle-2-al-menos.md"
codigo_relacionado:
  - "../codigo/capitulo-3-pregunta-08.ri"
escenario_ciudad:
  - av: 3
    ca: 2
    papeles: 1
  - av: 4
    ca: 2
    papeles: 1
  - av: 5
    ca: 2
    papeles: 1
  - av: 6
    ca: 2
    papeles: 1
  - av: 7
    ca: 2
    papeles: 1
  - av: 8
    ca: 2
    papeles: 1
  - av: 9
    ca: 2
    papeles: 1
  - av: 10
    ca: 2
    papeles: 1
  - av: 11
    ca: 2
    papeles: 1
  - av: 12
    ca: 2
    papeles: 1
---

# Solución: caminar la calle 2 hasta encontrar al menos 10 papeles

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-08-diez-papeles-calle-2-al-menos.md`](../ejercicios/ejercicio-08-diez-papeles-calle-2-al-menos.md).

## Análisis

Igual que en el ejercicio 5, como no se garantiza que existan 10 papeles, el corte del recorrido combina la condición de cantidad (`x<10`) con el límite de la calle (`PosAv<100`), para que el robot pueda terminar aunque no llegue a los 10 papeles.

## Estrategia

1. Posicionar el robot en (1,2) y girar a la derecha.
2. Mientras `PosAv<100`: si `x<10`, drenar todos los papeles de la esquina actual contándolos en `x`; avanzar (siempre).
3. Procesar la esquina final (avenida 100) por separado, sin avanzar.
4. Informar la posición final.

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
    Pos(1,2)
    x:=0
    derecha
    mientras(PosAv<100)
      si(x<10)
        mientras(HayPapelEnLaEsquina)
          tomarPapel
          x:=x+1
      mover
    si(x<10)
      mientras(HayPapelEnLaEsquina)
        tomarPapel
        x:=x+1
    Informar(PosAv,PosCa)
  fin
variables
  robin:robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/capitulo-3-pregunta-08.ri`](../codigo/capitulo-3-pregunta-08.ri)

## Correcciones aplicadas durante esta organización

Se aplicaron dos correcciones puntuales, verificadas ambas con el intérprete de R-info:

1. **`mover` mal anidado (mismo bug que `ejercicio-05`):** en el archivo histórico, `mover` estaba dentro del `si(x<10)`, así que en cuanto `x` llegaba a 10 antes de terminar la calle, `mover` dejaba de ejecutarse y `PosAv` quedaba congelado, dejando el `mientras(PosAv<100)` exterior colgado para siempre. Probado: con 10 papeles cargados entre las avenidas 3 y 12 de la calle 2, el archivo original se cuelga (supera el límite de pasos del intérprete); con `mover` desanidado (ejecutándose siempre, al mismo nivel que `si(x<10)`), el programa termina normalmente.
2. **Límite de la calle incompleto (`PosAv<99` en vez de `PosAv<100`):** con el límite original, el `mientras` sólo cubría las avenidas 1 a 98 dentro del bucle más la avenida 99 en el bloque final, dejando la avenida 100 sin revisar — la misma clase de problema que en `ejercicio-03`, pero acá se pudo corregir con un solo cambio porque el archivo ya tenía el bloque final (`si(x<10) mientras(HayPapelEnLaEsquina)...`) armado para procesar "la última esquina"; sólo hacía falta que el límite del `mientras` la dejara en la avenida correcta (100) para que ese bloque la cubriera. Se cambió `PosAv<99` por `PosAv<100`.

Con ambas correcciones aplicadas, se probó con 10 papeles en avenidas 3-12 (termina en (100,2)), sin papeles (termina en (100,2), `x` se queda en 0), y con 10 papeles en avenidas 91-100 (incluyendo la esquina límite, también termina en (100,2)) — en los tres casos el programa recorre la calle 2 completa sin colgarse ni salirse de la ciudad.

## Escenario de prueba

Cargar entre 1 y 15 papeles repartidos en la calle 2 para observar cómo el robot se detiene de contar apenas llega a 10 pero sigue caminando hasta el final de la calle. Probar también con cero papeles para confirmar que el recorrido termina igual.

## Casos límite

- Sin papeles en la calle: el robot recorre igual toda la calle 2 y termina en (100,2).
- Exactamente 10 papeles en la última esquina (avenida 100): se cuentan gracias al bloque final que procesa esa esquina por separado.

## Errores frecuentes

- El mismo problema de anidar `mover` dentro de una condición que puede volverse falsa antes de que el bucle exterior termine (ver `ejercicio-05`).
- Usar un límite de bucle "off by one" (99 en vez de 100) al querer cubrir una calle completa con el patrón `mientras(PosAv<N) + bloque final`.

## Complejidad

Recorrido de hasta 100 esquinas (una calle completa): O(1) respecto al tamaño de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-08-diez-papeles-calle-2-al-menos.md`](../ejercicios/ejercicio-08-diez-papeles-calle-2-al-menos.md)
- Código: [`../codigo/capitulo-3-pregunta-08.ri`](../codigo/capitulo-3-pregunta-08.ri)
