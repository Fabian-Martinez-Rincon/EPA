---
id: "EPA-U06-EJ02-ENUNCIADO"
titulo: "Ejercicio 2: recorridos de la figura 6.5 reutilizando el proceso cuadrado"
slug: "ejercicio-02-recorridos-de-cuadrados-con-proceso-parametrizado"
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
  - "../ejercicios/ejercicio-01-cuadrado-con-lado-como-parametro.md"
relacionados:
  - "../soluciones/ejercicio-02-recorridos-de-cuadrados-con-proceso-parametrizado.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_2B"
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_2C"
---

# Ejercicio 2: recorridos de la figura 6.5 reutilizando el proceso cuadrado

## Enunciado

Utilice el proceso de 1. (`cuadrado`, con la longitud del lado como parámetro de entrada) para realizar los recorridos de la figura 6.5 a partir de (1,1).

La figura 6.5 muestra dos recorridos distintos hechos con cuadrados de tamaño creciente, ambos a partir de la esquina (1,1):

- **a)** varios cuadrados de lado creciente (1, 2, 3, 4) compartiendo el mismo origen (1,1), unos "adentro" de otros.
- **b)** una hilera de cuadrados de lado creciente, cada uno apoyado junto al anterior sobre la misma calle, empezando en (1,1).

## Datos

- **Entradas:** ninguna leída en tiempo de ejecución; el punto de partida (1,1) y los tamaños de los cuadrados están fijos en el enunciado/figura.
- **Salidas:** ninguna; el resultado se observa en el recorrido trazado.
- **Restricciones:** debe reutilizarse el proceso `cuadrado(E lado:numero)` del ejercicio 1, sin reimplementar el trazado del cuadrado.

## Referencias

- Solución: [`../soluciones/ejercicio-02-recorridos-de-cuadrados-con-proceso-parametrizado.md`](../soluciones/ejercicio-02-recorridos-de-cuadrados-con-proceso-parametrizado.md)
- Código: [`../codigo/soluciones/capitulo-06/Cap6_Preg_2B`](../codigo/soluciones/capitulo-06/Cap6_Preg_2B) (recorrido a), [`../codigo/soluciones/capitulo-06/Cap6_Preg_2C`](../codigo/soluciones/capitulo-06/Cap6_Preg_2C) (recorrido b)
- Proceso base: [ejercicio 1](../ejercicios/ejercicio-01-cuadrado-con-lado-como-parametro.md)
- Figura: [`../recursos/figura-6-5-recorridos-cuadrados.png`](../recursos/figura-6-5-recorridos-cuadrados.png)
