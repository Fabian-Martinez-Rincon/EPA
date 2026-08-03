---
id: "EPA-U08-EJ01-ENUNCIADO"
titulo: "Ejercicio adicional 1: recorrer todas las avenidas hasta esquina vacía"
slug: "ejercicio-01-recorrer-avenidas-hasta-esquina-vacia"
tipo: "ejercicio"
unidad: 8
tema: "practica-adicional"
subtemas:
  - "modularizacion"
  - "parametros-de-salida"
nivel: "intermedio"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Ejercicios Adicionales.pdf"
    paginas: "1-2"
prerrequisitos:
  - "../../unidad-07-parametros-de-entrada-salida/capitulo-7-parametros-de-entrada-salida.md"
relacionados:
  - "../soluciones/ejercicio-01-recorrer-avenidas-hasta-esquina-vacia.md"
codigo_relacionado:
  - "../codigo/ejercicio-01.ri"
---

# Ejercicio adicional 1: recorrer todas las avenidas hasta esquina vacía

## Enunciado

Escriba un programa que le permita al robot recorrer todas las avenidas de la ciudad. Cada avenida debe recorrerse sólo hasta encontrar una esquina vacía (sin flor ni papel) que seguro existe. Además a medida que se recorre cada avenida debe informar si la misma tuvo a lo sumo 45 flores (hasta que encontró la esquina).

**Nota:** Se debe usar Modularización. "A lo sumo" = "como mucho" = "como máximo" = "máximo".

## Datos

- **Entradas:** ninguna leída en tiempo de ejecución; el estado de flores/papeles de la ciudad se configura antes de correr.
- **Salidas:** un `Informar(1)` o `Informar(0)` por cada una de las 100 avenidas, según haya tenido a lo sumo 45 flores hasta la esquina vacía.
- **Restricciones:** cada avenida tiene garantizado al menos una esquina sin flor ni papel.

## Referencias

- Solución: [`../soluciones/ejercicio-01-recorrer-avenidas-hasta-esquina-vacia.md`](../soluciones/ejercicio-01-recorrer-avenidas-hasta-esquina-vacia.md)
- Código: [`../codigo/ejercicio-01.ri`](../codigo/ejercicio-01.ri)
- Versión guiada con animación: [`../practica-guiada.md`](../practica-guiada.md)
