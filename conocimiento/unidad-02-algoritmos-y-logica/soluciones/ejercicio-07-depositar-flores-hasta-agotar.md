---
id: "EPA-U02-EJ07-SOLUCION"
titulo: "Solución: depositar flores en la avenida 10 hasta agotarlas"
slug: "ejercicio-07-depositar-flores-hasta-agotar"
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
  - "../ejercicios/ejercicio-07-depositar-flores-hasta-agotar.md"
codigo_relacionado:
  - "../codigo/ejercicio-07.ri"
escenario_bolsa:
  flores: 5
  papeles: 0
---

# Solución: depositar flores en la avenida 10 hasta agotarlas

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-07-depositar-flores-hasta-agotar.md`](../ejercicios/ejercicio-07-depositar-flores-hasta-agotar.md).

## Análisis

Es el mismo patrón condicional que el ejercicio 2 (avanzar depositando mientras haya con qué, seguir avanzando cuando no), aplicado al eje de avenidas: el robot se reposiciona en (10,1), gira una vez a la derecha para orientarse hacia avenidas crecientes, y recorre hasta la avenida 100.

## Estrategia

1. Reposicionar el robot en (10,1) con `Pos` y girar a la derecha (orientación hacia avenidas crecientes).
2. Mientras `PosAv < 100`: si hay flor en la bolsa, depositarla y avanzar; si no, avanzar igual.

## Código relacionado

```rinfo
programa prueba
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  comenzar
    Pos(10,1)
    derecha
    mientras (PosAv<100)
      si HayFlorEnLaBolsa
        depositarFlor
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

Código completo: [`../codigo/ejercicio-07.ri`](../codigo/ejercicio-07.ri)

## El recorrido va por la calle 1

El enunciado dice "avenida 10", pero el código arranca en (10,1), gira una vez a la derecha y avanza aumentando la avenida. O sea que recorre la calle 1, desde la avenida 10 hasta la 100. Para recorrer la avenida 10 de verdad, sacá el `derecha` (el robot ya arranca mirando al norte) y cambiá la condición a `mientras (PosCa<100)`.

## Escenario de prueba

Arrancá con flores en la bolsa, menos de 90. Vas a ver al robot dejando una por esquina hasta quedarse sin nada, y seguir caminando igual hasta el final.

## Casos límite

- La última esquina, (100,1), nunca recibe flor. El `mientras` corta cuando `PosAv` llega a 100, así que el último depósito cae en la avenida 99.
- Si te sobran flores al terminar no pasa nada. El enunciado no pide vaciar la bolsa.

## Errores frecuentes

- Escribir `mientras (PosAv<=100)`. Parado en la avenida 100 el robot intenta un `mover` más, se va de la ciudad y el programa corta con error.
- Sacar la rama `sino`. Apenas se vacía la bolsa el robot se queda clavado y nunca llega al final, que es justo lo que el enunciado pide evitar.

## Complejidad

Recorrido lineal de 90 esquinas (avenida 10 a 100): O(n) en el largo del tramo recorrido.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-07-depositar-flores-hasta-agotar.md`](../ejercicios/ejercicio-07-depositar-flores-hasta-agotar.md)
- Código: [`../codigo/ejercicio-07.ri`](../codigo/ejercicio-07.ri)
