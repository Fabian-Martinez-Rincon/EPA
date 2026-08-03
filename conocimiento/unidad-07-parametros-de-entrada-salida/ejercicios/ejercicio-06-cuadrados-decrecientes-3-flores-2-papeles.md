---
id: "EPA-U07-EJ06-ENUNCIADO"
titulo: "Ejercicio 6: recorrer cuadrados decrecientes hasta hallar 3 flores y 2 papeles"
slug: "ejercicio-06-cuadrados-decrecientes-3-flores-2-papeles"
tipo: "ejercicio"
unidad: 7
tema: "parametros-de-entrada-salida"
subtemas:
  - "parametro-e-y-es-combinados"
  - "primitivas-del-robot"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 7-Parametros de Entrada-Salida.pdf"
    paginas: "10"
prerrequisitos:
  - "../capitulo-7-parametros-de-entrada-salida.md"
relacionados:
  - "../soluciones/ejercicio-06-cuadrados-decrecientes-3-flores-2-papeles.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-07/Cap7_Preg_6"
---

# Ejercicio 6: recorrer cuadrados decrecientes hasta hallar 3 flores y 2 papeles

## Enunciado

Escriba un programa que le permita al robot recorrer cuadrados hasta encontrar un cuadrado con exactamente 3 flores y 2 papeles (seguro existe). El primer cuadrado es de lado 99 y los siguientes van decrementando en uno el tamaño del lado (98, 97 y así sucesivamente).

## Datos

- **Entradas:** ninguna leída en tiempo de ejecución; el lado del primer cuadrado (99) y el decremento (1) están fijos en el enunciado.
- **Salidas:** por cada cuadrado recorrido, el lado y las cantidades de flores y papeles halladas (`Informar`), hasta dar con el cuadrado que tiene exactamente 3 flores y 2 papeles.
- **Restricciones:** se garantiza que existe un cuadrado (de algún lado entre 1 y 99) con exactamente 3 flores y 2 papeles; el recorrido no debe modificar la cantidad de flores/papeles de las esquinas que va pisando.

## Referencias

- Solución: [`../soluciones/ejercicio-06-cuadrados-decrecientes-3-flores-2-papeles.md`](../soluciones/ejercicio-06-cuadrados-decrecientes-3-flores-2-papeles.md)
- Código: [`../codigo/soluciones/capitulo-07/Cap7_Preg_6`](../codigo/soluciones/capitulo-07/Cap7_Preg_6)
