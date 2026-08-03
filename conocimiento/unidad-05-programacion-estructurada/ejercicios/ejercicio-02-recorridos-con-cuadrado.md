---
id: "EPA-U05-EJ02-ENUNCIADO"
titulo: "Ejercicio 2: recorridos de la figura 5.9 usando el proceso cuadrado"
slug: "ejercicio-02-recorridos-con-cuadrado"
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
  - "../ejercicios/ejercicio-01-cuadrado-lado-2-horario.md"
relacionados:
  - "../soluciones/ejercicio-02-recorridos-con-cuadrado.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-05/Cap5_2A"
  - "../codigo/soluciones/capitulo-05/Cap5_2B"
---

# Ejercicio 2: recorridos de la figura 5.9 usando el proceso cuadrado

## Enunciado

Utilice el proceso desarrollado en el ejercicio 1 (un cuadrado de lado 2 en sentido horario) para realizar un programa para cada uno de los recorridos de la figura 5.9.

**Figura 5.9: Recorridos usando cuadrados de lado 2** ([recursos/figura-5-9-recorridos-cuadrados.png](../recursos/figura-5-9-recorridos-cuadrados.png)) — dos recorridos marcados a) y b), ambos partiendo de la esquina (1,1):

- a) tres cuadrados de lado 2 dispuestos en diagonal ascendente desde (1,1), cada uno tocando al siguiente por una única esquina (cada cuadrado arranca 3 esquinas más allá que el anterior, tanto en avenida como en calle).
- b) dos cuadrados de lado 2 apilados verticalmente, uno arriba del otro, alineados en la misma avenida (no en diagonal) y con un hueco entre ambos, sobre una grilla más pequeña que el recorrido a).

## Datos

- **Entradas:** ninguna leída en tiempo de ejecución; el punto de partida (1,1) es fijo en el enunciado.
- **Salidas:** ninguna; el resultado se observa en el recorrido trazado (posiciones de los distintos cuadrados de lado 2 sobre la ciudad).
- **Restricciones:** debe reutilizarse el proceso `cuadrado` del ejercicio 1, no reimplementar el trazado del cuadrado de cero.

## Referencias

- Solución: [`../soluciones/ejercicio-02-recorridos-con-cuadrado.md`](../soluciones/ejercicio-02-recorridos-con-cuadrado.md)
- Código: [`../codigo/soluciones/capitulo-05/Cap5_2A`](<../codigo/soluciones/capitulo-05/Cap5_2A>) (variante A), [`../codigo/soluciones/capitulo-05/Cap5_2B`](<../codigo/soluciones/capitulo-05/Cap5_2B>) (variante B)
- Prerrequisito: [ejercicio 1](ejercicio-01-cuadrado-lado-2-horario.md), que define el proceso `cuadrado` reutilizado acá.
