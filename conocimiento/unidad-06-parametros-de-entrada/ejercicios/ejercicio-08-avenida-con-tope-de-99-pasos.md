---
id: "EPA-U06-EJ08-ENUNCIADO"
titulo: "Ejercicio 8: recorrer una avenida una cantidad de pasos, con tope de 99"
slug: "ejercicio-08-avenida-con-tope-de-99-pasos"
tipo: "ejercicio"
unidad: 6
tema: "parametros-de-entrada"
subtemas:
  - "declaracion-de-parametros"
  - "restriccion-en-el-uso-de-parametros-de-entrada"
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
  - "../soluciones/ejercicio-08-avenida-con-tope-de-99-pasos.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_8"
---

# Ejercicio 8: recorrer una avenida una cantidad de pasos, con tope de 99

## Enunciado

Programe al robot para que realice un módulo Avenida que recorra una avenida, cuyo número se ingresa como parámetro, hasta dar tantos pasos como los indicados por otro parámetro de entrada que este módulo recibe. Es decir, si recibe los valores 3 y 1, debe dar 1 paso en la avenida 3; si recibe 12 y 5 debe dar 5 pasos en la avenida 12; y así sucesivamente. En cambio, si recibe algún valor negativo no debe dar pasos. Considere que la cantidad máxima de pasos que podrá dar es 99, cualquier valor que reciba mayor que 99, implicará realizar sólo hasta 99 pasos. Los números de avenida seguro son entre 1 y 100.

## Datos

- **Entradas:** el número de avenida y la cantidad de pasos a dar, ambos recibidos por el módulo como parámetros de entrada (`E`).
- **Salidas:** ninguna; el resultado se observa en la cantidad de cuadras que recorre el robot.
- **Restricciones:** valores negativos de pasos no deben mover al robot; valores mayores a 99 se acotan a 99; el número de avenida siempre es válido (entre 1 y 100), no requiere validación.

## Referencias

- Solución: [`../soluciones/ejercicio-08-avenida-con-tope-de-99-pasos.md`](../soluciones/ejercicio-08-avenida-con-tope-de-99-pasos.md)
- Código: [`../codigo/soluciones/capitulo-06/Cap6_Preg_8`](../codigo/soluciones/capitulo-06/Cap6_Preg_8)
