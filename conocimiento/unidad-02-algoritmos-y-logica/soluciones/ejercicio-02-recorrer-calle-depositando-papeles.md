---
id: "EPA-U02-EJ02-SOLUCION"
titulo: "Solución: recorrer la calle 50 depositando papeles"
slug: "ejercicio-02-recorrer-calle-depositando-papeles"
tipo: "solucion"
unidad: 2
tema: "algoritmos-logica-y-r-info"
subtemas:
  - "estructuras-de-control"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 2-Algoritmos y Logica.pdf"
    paginas: "1-30"
relacionados:
  - "../ejercicios/ejercicio-02-recorrer-calle-depositando-papeles.md"
codigo_relacionado:
  - "../codigo/ejercicio-02.ri"
escenario_bolsa:
  flores: 0
  papeles: 5
---

# Solución: recorrer la calle 50 depositando papeles

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-02-recorrer-calle-depositando-papeles.md`](../ejercicios/ejercicio-02-recorrer-calle-depositando-papeles.md).

## Análisis

El robot arranca en (1,1) y se reposiciona con `Pos(65,50)` al punto de partida real del enunciado. Girando tres veces a la derecha queda orientado hacia las avenidas decrecientes, así que avanzar (`mover`) con esa orientación baja `PosAv` manteniendo la calle fija en 50 — exactamente el eje que pide el enunciado (recorrer una calle, avenida variable).

## Estrategia

1. Reposicionar el robot en (65,50) con `Pos`.
2. Girar tres veces a la derecha para quedar orientado hacia avenidas decrecientes.
3. Mientras `PosAv > 23`: si hay papel en la bolsa, depositarlo antes de moverse; si no, moverse igual (para llegar hasta el final aunque se acaben los papeles).

## Código relacionado

```
programa prueba
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  comenzar
    Pos(65,50)
    repetir 3
      derecha
    mientras(PosAv>23)
      si  (HayPapelEnLaBolsa)
        depositarPapel
        mover
      sino
        mover
  fin
variables
  robin:robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/ejercicio-02.ri`](../codigo/ejercicio-02.ri)

## Corrección aplicada durante esta organización

El archivo histórico usaba `HayFlorEnLaBolsa`/`depositarFlor` en vez de `HayPapelEnLaBolsa`/`depositarPapel`, a pesar de que el enunciado (y el propio comentario `{...}` del archivo) hablan de papeles — muy probablemente un copy-paste sin actualizar desde otro ejercicio de flores. Se corrigió el tipo de objeto sin tocar la estructura de control ni el resto de la lógica.

## Escenario de prueba

Para observar el efecto hace falta que algunas esquinas entre (65,50) y (23,50) tengan papel en la bolsa del robot al iniciar la simulación (la bolsa arranca vacía salvo que el visor la precargue) — con la bolsa vacía el programa igual termina, solo que sin depositar nada, porque la rama `sino: mover` cubre ese caso explícitamente.

## Casos límite

- Bolsa vacía desde el inicio: el robot igual completa el recorrido hasta la avenida 23 (rama `sino`), sin depositar nada.
- El robot nunca se pasa de la avenida 23: la condición de corte es `PosAv > 23`, así que la esquina (23,50) queda fuera del recorrido de depósito.

## Errores frecuentes

- Confundir flor y papel al escribir la condición/la primitiva (el bug real que tenía este archivo antes de esta organización).
- Usar `mientras` sin la rama `sino` para el caso "sin papeles", lo que dejaría al robot detenido apenas se vacía la bolsa en vez de seguir hasta el final.

## Complejidad

Un solo recorrido lineal de a lo sumo 42 esquinas (de avenida 65 a 23): O(n) en la distancia entre punto de partida y de llegada.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-02-recorrer-calle-depositando-papeles.md`](../ejercicios/ejercicio-02-recorrer-calle-depositando-papeles.md)
- Fuente original: [`../fuentes/Capitulo 2-Algoritmos y Logica.pdf`](<../fuentes/Capitulo 2-Algoritmos y Logica.pdf>)
- Código: [`../codigo/ejercicio-02.ri`](../codigo/ejercicio-02.ri)
