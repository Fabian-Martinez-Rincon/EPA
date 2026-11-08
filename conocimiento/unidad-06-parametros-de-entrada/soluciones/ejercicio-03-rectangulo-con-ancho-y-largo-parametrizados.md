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

```rinfo
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

Ciudad vacía, sin flores ni papeles. Con `anchx:=4` y `largx:=10`, el robot sube 10 cuadras desde (1,1), dobla y avanza 4 hasta (5,11), baja otras 10 hasta (5,1) y vuelve a (1,1).

## Casos límite

- Si le pasás el mismo valor a los dos parámetros, el proceso dibuja un cuadrado. No hace falta ningún caso especial: un cuadrado es un rectángulo.
- Con `anchx:=0` el rectángulo se aplasta a una línea. El robot sube 10, gira dos veces sin avanzar, baja las mismas 10 y termina en (1,1). El proceso no falla.

## Errores frecuentes

- Poner los dos `repetir largo` seguidos en vez de alternar `largo` y `ancho`. El robot traza dos lados paralelos y la figura nunca cierra.
- Olvidar el segundo `derecha` de cada vuelta. El lado siguiente sale en la dirección equivocada y el rectángulo se deforma.

## Complejidad

El recorrido tiene `2 × (ancho + largo)` pasos: O(ancho + largo) respecto de los parámetros recibidos.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-03-rectangulo-con-ancho-y-largo-parametrizados.md`](../ejercicios/ejercicio-03-rectangulo-con-ancho-y-largo-parametrizados.md)
- Código: [`../codigo/soluciones/capitulo-06/Cap6_Preg_3`](../codigo/soluciones/capitulo-06/Cap6_Preg_3)
