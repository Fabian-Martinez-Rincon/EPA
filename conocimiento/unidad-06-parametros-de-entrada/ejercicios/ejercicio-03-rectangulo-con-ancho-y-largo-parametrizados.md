---
id: "EPA-U06-EJ03-ENUNCIADO"
titulo: "Ejercicio 3: rectángulo con ancho y largo como parámetros"
slug: "ejercicio-03-rectangulo-con-ancho-y-largo-parametrizados"
tipo: "ejercicio"
unidad: 6
tema: "parametros-de-entrada"
subtemas:
  - "declaracion-de-parametros"
  - "comunicacion-entre-modulos"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 6-Parametros de Entrada.pdf"
    paginas: "1-20"
prerrequisitos:
  - "../capitulo-6-parametros-de-entrada.md"
relacionados:
  - "../soluciones/ejercicio-03-rectangulo-con-ancho-y-largo-parametrizados.md"
  - "../ejercicios/ejercicio-04-recorridos-de-rectangulos-con-proceso-parametrizado.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_3"
---

# Ejercicio 3: rectángulo con ancho y largo como parámetros

## Enunciado

Escriba un proceso que le permita al Robot realizar un rectángulo a partir de la esquina donde está parado cuyas dimensiones, alto y ancho, se reciben.

## Datos

- **Entradas:** las dos dimensiones del rectángulo (ancho y largo/alto), recibidas por el proceso a través de dos parámetros de entrada (`E`).
- **Salidas:** ninguna; el resultado se observa en el recorrido que traza el robot.
- **Restricciones:** el rectángulo debe comenzar en la esquina donde el robot ya está parado al momento de invocar el proceso.

## Referencias

- Solución: [`../soluciones/ejercicio-03-rectangulo-con-ancho-y-largo-parametrizados.md`](../soluciones/ejercicio-03-rectangulo-con-ancho-y-largo-parametrizados.md)
- Código: [`../codigo/soluciones/capitulo-06/Cap6_Preg_3`](../codigo/soluciones/capitulo-06/Cap6_Preg_3)
- Este proceso `rectangulo` es reutilizado por el [ejercicio 4](../ejercicios/ejercicio-04-recorridos-de-rectangulos-con-proceso-parametrizado.md).
