---
id: "EPA-U02-EJ06-SOLUCION"
titulo: "Solución: recorrer la avenida 75 recogiendo flores"
slug: "ejercicio-06-recorrer-avenida-recogiendo-flores"
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
  - "../ejercicios/ejercicio-06-recorrer-avenida-recogiendo-flores.md"
codigo_relacionado:
  - "../codigo/ejercicio-06.ri"
escenario_ciudad:
  - av: 75
    ca: 45
    flores: 1
    papeles: 0
  - av: 75
    ca: 30
    flores: 1
    papeles: 0
  - av: 75
    ca: 16
    flores: 1
    papeles: 0
---

# Solución: recorrer la avenida 75 recogiendo flores

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-06-recorrer-avenida-recogiendo-flores.md`](../ejercicios/ejercicio-06-recorrer-avenida-recogiendo-flores.md).

## Análisis

Es el mismo patrón que el ejercicio 2 pero en el eje de calles: reposicionarse en el punto de partida, girar 180° (dos `derecha`) para orientarse hacia calles decrecientes, y recorrer hasta la calle destino levantando flores en el camino.

## Estrategia

1. Reposicionar el robot en (75,45) con `Pos`.
2. Girar dos veces a la derecha para quedar orientado hacia calles decrecientes.
3. Mientras `PosCa > 15`: si hay flor en la esquina, tomarla y avanzar; si no, avanzar directamente.

## Código relacionado

```
programa prueba
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  comenzar
    Pos(75,45)
    repetir 2
      derecha
    mientras (PosCa>15)
      si HayFlorEnLaEsquina
        tomarFlor
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

Código completo: [`../codigo/ejercicio-06.ri`](../codigo/ejercicio-06.ri)

## Escenario de prueba

Para ver el efecto conviene que alguna esquina entre (75,45) y (75,15) tenga flor al iniciar la simulación; sin flores cargadas el robot igual completa el recorrido, solo que no levanta nada.

## Casos límite

- Ninguna esquina con flor en el camino: el robot llega igual a la calle 15, sin levantar nada.
- La esquina (75,15) queda fuera del recorrido: la condición de corte es `PosCa > 15`.

## Errores frecuentes

- Girar una sola vez en vez de dos, lo que orientaría al robot hacia el eje de avenidas en vez del eje de calles.
- Olvidar la rama `sino` y quedar sin avanzar en las esquinas sin flor.

## Complejidad

Recorrido lineal de 30 esquinas (calle 45 a calle 15): O(n) en la distancia entre origen y destino.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-06-recorrer-avenida-recogiendo-flores.md`](../ejercicios/ejercicio-06-recorrer-avenida-recogiendo-flores.md)
- Código: [`../codigo/ejercicio-06.ri`](../codigo/ejercicio-06.ri)
