---
id: "EPA-U06-EJ03-SOLUCION"
titulo: "Solución: rectángulo con ancho y largo como parámetros"
slug: "ejercicio-03-rectangulo-con-ancho-y-largo-parametrizados"
tipo: "solucion"
unidad: 6
tema: "parametros-de-entrada"
subtemas:
  - "declaracion-de-parametros"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 6-Parametros de Entrada.pdf"
    paginas: "1-20"
relacionados:
  - "../ejercicios/ejercicio-03-rectangulo-con-ancho-y-largo-parametrizados.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_3"
---

# Solución: rectángulo con ancho y largo como parámetros

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-03-rectangulo-con-ancho-y-largo-parametrizados.md`](../ejercicios/ejercicio-03-rectangulo-con-ancho-y-largo-parametrizados.md).

## Análisis

Un rectángulo es como un cuadrado (ejercicio 1) pero alternando dos longitudes de lado en vez de una sola. El proceso recibe dos parámetros de entrada, `ancho` y `largo`, y traza dos veces el par de lados "largo, ancho" girando 90° después de cada uno — cuatro giros en total, que cierran el rectángulo exactamente donde empezó.

Los nombres de los parámetros formales (`ancho`, `largo`) no necesitan coincidir con las palabras del enunciado ("alto y ancho"): lo que importa es que ambos sean parámetros de entrada numéricos, cada uno gobernando un par de lados opuestos del rectángulo, tal como ya se explica en el Ejemplo 6.4 del capítulo (que usa los nombres `base` y `altura` para el mismo patrón).

## Estrategia

1. Declarar `proceso rectangulo(E ancho:numero; E largo:numero)`.
2. Repetir 2 veces: avanzar `largo` cuadras, girar a la derecha, avanzar `ancho` cuadras, girar a la derecha.
3. Invocar `rectangulo(anchx,largx)` desde el programa principal con las dimensiones deseadas.

## Código relacionado

```
programa  parametros
procesos
  proceso rectangulo(E ancho:numero; E largo:numero)
  comenzar
    repetir 2
      repetir largo
        mover
      derecha
      repetir ancho
        mover
      derecha
  fin
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  variables
    anchx:numero
    largx:numero
  comenzar
    anchx:=4
    largx:=10
    rectangulo(anchx,largx)  
  fin
variables
  robin: robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-06/Cap6_Preg_3`](../codigo/soluciones/capitulo-06/Cap6_Preg_3)

## Escenario de prueba

No requiere flores ni papeles precargados: alcanza con observar que, partiendo de (1,1), el robot traza un rectángulo de 4 de ancho por 10 de largo y regresa a su esquina de origen.

## Casos límite

- `ancho = largo`: el proceso dibuja un cuadrado, sin que haga falta ningún caso especial (un cuadrado es un rectángulo particular).
- Ninguno de los dos parámetros se modifica dentro del proceso: ambos son de entrada (`E`) y solo se leen para controlar los `repetir` internos, respetando la restricción de la sección 6.5 del capítulo.

## Errores frecuentes

- Repetir el mismo lado dos veces seguidas en vez de alternar `largo`/`ancho`, lo que trazaría dos segmentos paralelos en vez de un rectángulo cerrado.
- Olvidar el segundo `derecha` de cada mitad del `repetir 2`, dejando al robot mal orientado para el lado siguiente.

## Complejidad

El recorrido tiene `2 × (ancho + largo)` pasos: O(ancho + largo) respecto de los parámetros recibidos.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-03-rectangulo-con-ancho-y-largo-parametrizados.md`](../ejercicios/ejercicio-03-rectangulo-con-ancho-y-largo-parametrizados.md)
- Código: [`../codigo/soluciones/capitulo-06/Cap6_Preg_3`](../codigo/soluciones/capitulo-06/Cap6_Preg_3)
