---
id: "EPA-U06-EJ06-ENUNCIADO"
titulo: "Ejercicio 6: recorrer avenidas con el número como parámetro"
slug: "ejercicio-06-recorrer-avenidas-con-numero-parametrizado"
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
  - "../soluciones/ejercicio-06-recorrer-avenidas-con-numero-parametrizado.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_6A"
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_6B"
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_6C"
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_6D"
---

# Ejercicio 6: recorrer avenidas con el número como parámetro

## Enunciado

**a)** Escriba un proceso que le permita al robot recorrer una avenida cuyo número se ingresa como parámetro de entrada.

**b)** Utilice el proceso de 6.a) para recorrer todas las avenidas de la ciudad.

**c)** Utilice el proceso de 6.a) para recorrer las avenidas 5, 6, 7 … 15.

**d)** Utilice el proceso de 6.a) para recorrer las avenidas pares de la ciudad.

## Datos

- **Entradas:** el número de avenida a recorrer, recibido por el proceso base (6.a) a través de un parámetro de entrada (`E`); en 6.b/c/d ese número lo genera el programa principal en cada invocación sucesiva.
- **Salidas:** ninguna; el resultado se observa en el recorrido trazado.
- **Restricciones:** las partes b, c y d deben reutilizar el proceso de la parte a, sin reimplementar el recorrido de una avenida individual.

## Referencias

- Solución: [`../soluciones/ejercicio-06-recorrer-avenidas-con-numero-parametrizado.md`](../soluciones/ejercicio-06-recorrer-avenidas-con-numero-parametrizado.md)
- Código: [`../codigo/soluciones/capitulo-06/Cap6_Preg_6A`](../codigo/soluciones/capitulo-06/Cap6_Preg_6A) (a), [`../codigo/soluciones/capitulo-06/Cap6_Preg_6B`](../codigo/soluciones/capitulo-06/Cap6_Preg_6B) (b), [`../codigo/soluciones/capitulo-06/Cap6_Preg_6C`](../codigo/soluciones/capitulo-06/Cap6_Preg_6C) (c), [`../codigo/soluciones/capitulo-06/Cap6_Preg_6D`](../codigo/soluciones/capitulo-06/Cap6_Preg_6D) (d)
