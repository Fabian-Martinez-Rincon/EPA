---
id: "EPA-U06-EJ04-ENUNCIADO"
titulo: "Ejercicio 4: recorridos de la figura 6.6 reutilizando el proceso rectángulo"
slug: "ejercicio-04-recorridos-de-rectangulos-con-proceso-parametrizado"
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
  - "../ejercicios/ejercicio-03-rectangulo-con-ancho-y-largo-parametrizados.md"
relacionados:
  - "../soluciones/ejercicio-04-recorridos-de-rectangulos-con-proceso-parametrizado.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_4A"
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_4B"
---

# Ejercicio 4: recorridos de la figura 6.6 reutilizando el proceso rectángulo

## Enunciado

Utilice el proceso realizado en 3. (`rectangulo`, con ancho y largo como parámetros de entrada) para que el Robot efectúe los recorridos de la figura 6.6 a partir de (1,1).

La figura 6.6 muestra dos recorridos hechos con rectángulos de tamaño decreciente, ambos a partir de (1,1):

- **a)** una serie de rectángulos apilados hacia arriba, el más ancho abajo (cerca de (1,1)) y cada vez más angosto a medida que se sube.
- **b)** una columna angosta y alta formada por rectángulos apilados, todos de ancho mínimo pero de altura decreciente.

## Datos

- **Entradas:** ninguna leída en tiempo de ejecución; los tamaños y la cantidad de rectángulos están fijos en el enunciado/figura.
- **Salidas:** ninguna; el resultado se observa en el recorrido trazado.
- **Restricciones:** debe reutilizarse el proceso `rectangulo(E ancho:numero; E largo:numero)` del ejercicio 3.

## Referencias

- Solución: [`../soluciones/ejercicio-04-recorridos-de-rectangulos-con-proceso-parametrizado.md`](../soluciones/ejercicio-04-recorridos-de-rectangulos-con-proceso-parametrizado.md)
- Código: [`../codigo/soluciones/capitulo-06/Cap6_Preg_4A`](../codigo/soluciones/capitulo-06/Cap6_Preg_4A) (recorrido a), [`../codigo/soluciones/capitulo-06/Cap6_Preg_4B`](../codigo/soluciones/capitulo-06/Cap6_Preg_4B) (recorrido b)
- Proceso base: [ejercicio 3](../ejercicios/ejercicio-03-rectangulo-con-ancho-y-largo-parametrizados.md)
- Figura: [`../recursos/figura-6-6-recorridos-rectangulos.png`](../recursos/figura-6-6-recorridos-rectangulos.png)
