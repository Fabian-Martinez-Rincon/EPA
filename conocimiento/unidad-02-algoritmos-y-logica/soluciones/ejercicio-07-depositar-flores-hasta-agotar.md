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

```
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

## Escenario de prueba

Conviene iniciar la simulación con algunas flores en la bolsa del robot para ver el depósito en acción; con menos flores que esquinas en la avenida 10, se puede observar cómo el robot sigue caminando sin depositar una vez que se queda sin flores, en vez de detenerse.

## Casos límite

- Bolsa vacía desde el inicio: el robot recorre toda la avenida sin depositar nada (rama `sino`).
- Más flores que esquinas: sobran flores en la bolsa al llegar a la avenida 100, lo cual es válido, el enunciado no pide vaciar la bolsa por completo.
- La esquina (10,100) sí recibe flor si hay disponible: la condición de corte es `PosAv < 100`, así que la última iteración deposita en la esquina 99 y el `mover` final la deja en 100 sin evaluar el depósito ahí — vale la pena confirmarlo al ejecutar, es un límite exacto fácil de errar.

## Errores frecuentes

- Cortar el `mientras` con `<=100` en vez de `<100`, lo que haría que el robot intente moverse una vez de más y quede fuera del área válida.
- Olvidar la rama `sino`, dejando al robot detenido en la primera esquina sin flores.

## Complejidad

Recorrido lineal de 90 esquinas (avenida 10 a 100): O(n) en el largo del tramo recorrido.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-07-depositar-flores-hasta-agotar.md`](../ejercicios/ejercicio-07-depositar-flores-hasta-agotar.md)
- Código: [`../codigo/ejercicio-07.ri`](../codigo/ejercicio-07.ri)
