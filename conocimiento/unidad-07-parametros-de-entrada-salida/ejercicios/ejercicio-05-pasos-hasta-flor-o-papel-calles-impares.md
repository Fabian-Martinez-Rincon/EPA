---
id: "EPA-U07-EJ05-ENUNCIADO"
titulo: "Ejercicio 5: pasos hasta encontrar flor o papel en cada calle impar"
slug: "ejercicio-05-pasos-hasta-flor-o-papel-calles-impares"
tipo: "ejercicio"
unidad: 7
tema: "parametros-de-entrada-salida"
subtemas:
  - "parametro-es-como-salida"
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
  - "../soluciones/ejercicio-05-pasos-hasta-flor-o-papel-calles-impares.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-07/Cap7_Preg_5"
---

# Ejercicio 5: pasos hasta encontrar flor o papel en cada calle impar

## Enunciado

Escriba un programa que le permita al robot recorrer las calles impares de la ciudad. Cada calle debe recorrerse sólo hasta encontrar una esquina con alguna flor o algún papel o ambos, que seguro existe. Al finalizar cada calle debe informarse cuantos pasos se ha dado hasta encontrar la esquina.

## Datos

- **Entradas:** ninguna leída en tiempo de ejecución; el conjunto de calles a recorrer (todas las impares, 1 a 99) está fijo en el enunciado.
- **Salidas:** por cada calle impar, la cantidad de pasos dados hasta encontrar la primera esquina con flor y/o papel, informada con `Informar`.
- **Restricciones:** cada calle impar tiene garantizada al menos una esquina con flor o papel (si no la tuviera, el recorrido llegaría hasta el final de la calle sin encontrar nada).

## Referencias

- Solución: [`../soluciones/ejercicio-05-pasos-hasta-flor-o-papel-calles-impares.md`](../soluciones/ejercicio-05-pasos-hasta-flor-o-papel-calles-impares.md)
- Código: [`../codigo/soluciones/capitulo-07/Cap7_Preg_5`](../codigo/soluciones/capitulo-07/Cap7_Preg_5)
