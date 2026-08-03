---
id: "EPA-U05-EJ04-ENUNCIADO"
titulo: "Ejercicio 4: recorridos de la figura 5.10 usando el proceso rectángulo"
slug: "ejercicio-04-recorridos-con-rectangulo"
tipo: "ejercicio"
unidad: 5
tema: "programacion-estructurada"
subtemas:
  - "programacion-modular"
  - "reusabilidad-de-procesos"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 5-Programacion Estructurada.pdf"
    paginas: "1-24"
prerrequisitos:
  - "../ejercicios/ejercicio-03-rectangulo-5x3-horario.md"
relacionados:
  - "../soluciones/ejercicio-04-recorridos-con-rectangulo.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-05/Cap5_4A"
  - "../codigo/soluciones/capitulo-05/Cap5_4B"
  - "../codigo/soluciones/capitulo-05/Cap5_4C"
  - "../codigo/soluciones/capitulo-05/Cap5_4C otro"
---

# Ejercicio 4: recorridos de la figura 5.10 usando el proceso rectángulo

## Enunciado

Programe al Robot para que realice los recorridos de la figura 5.10 utilizando el proceso desarrollado en el ejercicio 3.

**Figura 5.10: Recorridos usando rectángulos de 5x3** ([recursos/figura-5-10-recorridos-rectangulos.png](../recursos/figura-5-10-recorridos-rectangulos.png)) — tres recorridos marcados a), b) y c), todos partiendo de la esquina (1,1):

- a) cuatro rectángulos de 5x3 apilados verticalmente uno sobre otro, formando una columna.
- b) varios rectángulos de 5x3 entrelazados en diagonal, formando una figura escalonada compacta.
- c) una fila de varios rectángulos de 5x3 alineados horizontalmente uno junto a otro.

## Datos

- **Entradas:** ninguna leída en tiempo de ejecución; el punto de partida (1,1) es fijo en el enunciado.
- **Salidas:** ninguna; el resultado se observa en el recorrido trazado.
- **Restricciones:** debe reutilizarse el proceso `rectangulo` del ejercicio 3, no reimplementar el trazado del rectángulo de cero.

## Referencias

- Solución: [`../soluciones/ejercicio-04-recorridos-con-rectangulo.md`](../soluciones/ejercicio-04-recorridos-con-rectangulo.md)
- Código: [`../codigo/soluciones/capitulo-05/Cap5_4A`](<../codigo/soluciones/capitulo-05/Cap5_4A>) (recorrido a), [`../codigo/soluciones/capitulo-05/Cap5_4B`](<../codigo/soluciones/capitulo-05/Cap5_4B>) (recorrido b), [`../codigo/soluciones/capitulo-05/Cap5_4C`](<../codigo/soluciones/capitulo-05/Cap5_4C>) y [`../codigo/soluciones/capitulo-05/Cap5_4C otro`](<../codigo/soluciones/capitulo-05/Cap5_4C otro>) (dos implementaciones distintas del recorrido c)
- Prerrequisito: [ejercicio 3](ejercicio-03-rectangulo-5x3-horario.md), que define el proceso `rectangulo` reutilizado acá.
