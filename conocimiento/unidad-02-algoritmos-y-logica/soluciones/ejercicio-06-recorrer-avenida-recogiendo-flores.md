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

```rinfo
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

Poné flores en algunas esquinas de la avenida 75, entre la calle 45 y la calle 16. El robot va bajando y las levanta hasta llegar a la calle 15.

## Casos límite

- La flor que haya en (75,15) se queda ahí. El `mientras` corta al llegar a la calle 15, antes de mirar esa esquina.
- Si una esquina tiene dos flores, el robot se lleva una sola. El `si` ejecuta `tomarFlor` una vez por esquina; con `mientras (HayFlorEnLaEsquina)` las levantaría todas, que es lo que pide el enunciado.

## Errores frecuentes

- Girar una sola vez. Con un `derecha` el robot queda mirando al este y termina recorriendo la calle 45, no la avenida 75.
- Sacar la rama `sino`. En la primera esquina sin flor el robot deja de moverse y el `mientras` no termina más.

## Complejidad

Recorrido lineal de 30 esquinas (calle 45 a calle 15): O(n) en la distancia entre origen y destino.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-06-recorrer-avenida-recogiendo-flores.md`](../ejercicios/ejercicio-06-recorrer-avenida-recogiendo-flores.md)
- Código: [`../codigo/ejercicio-06.ri`](../codigo/ejercicio-06.ri)
