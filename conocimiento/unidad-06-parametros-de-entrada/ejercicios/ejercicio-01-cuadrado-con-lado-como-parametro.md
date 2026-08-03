---
id: "EPA-U06-EJ01-ENUNCIADO"
titulo: "Ejercicio 1: cuadrado con la longitud del lado como parámetro"
slug: "ejercicio-01-cuadrado-con-lado-como-parametro"
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
  - "../soluciones/ejercicio-01-cuadrado-con-lado-como-parametro.md"
  - "../ejercicios/ejercicio-02-recorridos-de-cuadrados-con-proceso-parametrizado.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_1"
---

# Ejercicio 1: cuadrado con la longitud del lado como parámetro

## Enunciado

Escriba un proceso que le permita al robot realizar un cuadrado a partir de la esquina donde está parado, girando en la dirección de las agujas del reloj y recibiendo como dato la longitud del lado.

## Datos

- **Entradas:** la longitud del lado del cuadrado, recibida por el proceso a través de un parámetro de entrada (`E`).
- **Salidas:** ninguna; el resultado se observa en el recorrido que traza el robot sobre la ciudad.
- **Restricciones:** el robot debe girar en el sentido de las agujas del reloj (es decir, usando `derecha`) y el cuadrado debe comenzar en la esquina donde el robot ya está parado al momento de invocar el proceso.

## Referencias

- Solución: [`../soluciones/ejercicio-01-cuadrado-con-lado-como-parametro.md`](../soluciones/ejercicio-01-cuadrado-con-lado-como-parametro.md)
- Código: [`../codigo/soluciones/capitulo-06/Cap6_Preg_1`](../codigo/soluciones/capitulo-06/Cap6_Preg_1)
- Este proceso `cuadrado` es reutilizado por el [ejercicio 2](../ejercicios/ejercicio-02-recorridos-de-cuadrados-con-proceso-parametrizado.md).
