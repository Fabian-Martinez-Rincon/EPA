---
id: "EPA-U02-EJ07-ENUNCIADO"
titulo: "Ejercicio 7: depositar flores en la avenida 10 hasta agotarlas"
slug: "ejercicio-07-depositar-flores-hasta-agotar"
tipo: "ejercicio"
unidad: 2
tema: "algoritmos-logica-y-r-info"
subtemas:
  - "estructuras-de-control"
  - "primitivas-del-robot"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 2-Algoritmos y Logica.pdf"
    paginas: "1-30"
prerrequisitos:
  - "../capitulo-2-algoritmos-y-logica.md"
relacionados:
  - "../soluciones/ejercicio-07-depositar-flores-hasta-agotar.md"
codigo_relacionado:
  - "../codigo/ejercicio-07.ri"
---

# Ejercicio 7: depositar flores en la avenida 10 hasta agotarlas

## Enunciado

Escriba un programa que le permita al robot recorrer la avenida 10, depositando una flor en cada esquina. Si en algún momento del recorrido se queda sin flores en la bolsa, debe seguir caminando (sin depositar) hasta terminar la avenida.

## Datos

- **Entradas:** ninguna leída en tiempo de ejecución.
- **Salidas:** ninguna; el resultado se observa en las flores depositadas a lo largo de la avenida 10.
- **Restricciones:** el robot debe llegar hasta el final de la avenida aunque se quede sin flores antes de terminar.

## Referencias

- Solución: [`../soluciones/ejercicio-07-depositar-flores-hasta-agotar.md`](../soluciones/ejercicio-07-depositar-flores-hasta-agotar.md)
- Código: [`../codigo/ejercicio-07.ri`](../codigo/ejercicio-07.ri)

## Nota sobre variantes no atomizadas

El capítulo trae tres archivos adicionales (`codigo/ejercicio-07-1.ri`, `ejercicio-07-4.ri`, `ejercicio-07-5.ri`) con el mismo comentario de enunciado que este ejercicio, pero que en realidad implementan problemas distintos (contar flores/papeles por avenida e informar totales) — no son variantes de este ejercicio, sino código mal etiquetado. Quedan sin atomizar, señalados como pendientes de investigación en el README de la unidad, igual que `codigo-01.ri`…`codigo-10.ri`.
