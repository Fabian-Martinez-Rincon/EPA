---
id: "CON-EPA-U08-EJERCICIOS-ADICIONALES"
titulo: "Ejercicios adicionales y exámenes voluntarios"
slug: "ejercicios-adicionales"
tipo: "ejercicio"
unidad: 8
tema: "practica-adicional"
subtemas:
  - "ejercicios-de-modularizacion"
  - "examenes-2013"
nivel: "intermedio"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "fuentes/Ejercicios Adicionales.pdf"
    paginas: "1-2"
prerrequisitos:
  - "CON-EPA-U07-PARAMETROS-ENTRADA-SALIDA"
relacionados:
  - "../unidad-07-parametros-de-entrada-salida/capitulo-7-parametros-de-entrada-salida.md"
codigo_relacionado:
  - "codigo"
---

# Ejercicios Adicionales

*Curso de Ingreso – Expresión de Problemas y Algoritmos (Facultad de Informática, UNLP). Versión: 2 - Ejercicios Adicionales. Páginas 148-149.*

1. Escriba un programa que le permita al robot recorrer todas las avenidas de la ciudad. Cada avenida debe recorrerse sólo hasta encontrar una esquina vacía (sin flor ni papel) que seguro existe. Además a medida que se recorre cada avenida debe informar si la misma tuvo a lo sumo 45 flores (hasta que encontró la esquina).

   **Nota:** Se debe usar Modularización.

2. Escriba un programa que le permita al robot recorrer todas las avenidas de la ciudad. Al finalizar el recorrido debe informar la cantidad de esquinas con exactamente 20 flores y la cantidad avenidas con menos de 60 papeles.

   **Nota:** Se debe usar Modularización y no modificar la cantidad de papeles/flores de las esquinas.

3. Escriba un programa que le permita al robot realizar el siguiente recorrido, comenzando en la esquina (1,1) juntando todas las flores y papeles de cada esquina. Al finalizar el recorrido debe informar la cantidad total de flores y de papeles que tiene en la bolsa.

   **Nota:** Se debe usar Modularización.

   ![Recorrido escalonado del ejercicio adicional 3](assets/adicional-ejercicio-3-recorrido.png)

   **Descripción accesible:** grilla de esquinas con un recorrido rojo en forma de escalera que comienza en **(1,1)** y aumenta progresivamente su extensión.

4. Programe al robot para que recorra la ciudad por avenidas, juntando papeles, hasta encontrar una avenida con exactamente 25 flores. Cuando encuentra la avenida con exactamente 25 flores debe recorrer toda la calle 75 (desde la avenida 1) y dar tantos pasos como papeles juntó en todas las avenidas recorridas.

   **Nota:** la avenida con 25 flores seguro existe. La cantidad de papeles juntados (entre todas las avenidas recorridas) seguro es menor a 100. Las esquinas pueden modificarse. Modularizar.

   **Ejemplo:** suponga que el robot encuentra que la avenida 5 tiene exactamente 25 flores, y durante su recorrido (avenidas 1, 2, 3, 4 y 5) juntó 62 papeles. Entonces debe recorrer la calle 75 y dar 62 pasos.

5. Escriba un programa que le permita al robot recorrer 10 calles de la ciudad (como se muestra en la figura). En cada calle debe juntar las flores y los papeles. Al finalizar cada calle informar la cantidad de esquinas con el doble de flores que papeles. Al finalizar el recorrido debe informar la cantidad total de papeles y de flores recogidas. El recorrido comienza en (1,1). En la primer calle se deben recorrer 8 avenidas, en la siguiente 2 avenidas más (es decir 10 avenidas) y así incrementar de a dos avenidas para las calles restantes.

   **Nota:** se debe usar Modularización.

   ![Calles de longitud creciente del ejercicio adicional 5](assets/adicional-ejercicio-5-recorrido.png)

   **Descripción accesible:** simulador R-info con diez recorridos horizontales de longitud creciente, iniciados desde el margen izquierdo de la ciudad.

6. Realice un programa para que el robot recorra 15 cuadrados los cuales comienzan siempre en la esquina (1,1). En cada cuadrado debe juntar las flores y los papeles. Al finalizar los 15 cuadrados debe informar cuántos cuadrados tenían más de 20 flores.

   **Notas:** Modularice. Se pide que como mínimo exista un módulo que realice un cuadrado. El primer cuadrado debe ser de lado 1, el segundo de lado 2 y así sucesivamente hasta llegar al cuadrado 15 el cual es de lado 15.

7. **EXAMEN AÑO 2013:** Escriba un algoritmo para que el robot recorra la avenida 8 juntando todas las flores y todos los papeles hasta encontrar una esquina vacía. Luego debe recorrer un rectángulo que comience en (1,1), donde el alto del rectángulo es igual a la cantidad de flores juntadas en la avenida 8 y el ancho o base es igual a la cantidad de papeles juntados en la avenida 8.

   **Ejemplo:** si cuando el robot termina de recorrer la avenida 8 (porque encontró la esquina vacía) juntó 5 flores y 4 papeles, debe posicionarse en (1,1) y hacer un rectángulo donde el alto es 5 y el ancho es 4.

   **Nota:** SE DEBE USAR MODULARIZACION (como mínimo debe haber un módulo para la avenida 8, y otro para el rectángulo). LA ESQUINA VACIA DE LA AVENIDA 8 SEGURO EXISTE. EL TOTAL DE FLORES Y DE PAPELES DE LA AVENIDA 8 <= 99.

8. **EXAMEN AÑO 2013:** Escriba un algoritmo para que el robot recorra las calles impares de la ciudad. Cada calle debe recorrerse hasta juntar al menos 10 flores. Una vez que ha recorrido todas las calles debe recorrer la avenida 10, la avenida 11 y la avenida 12 juntando todos los papeles. Al finalizar de recorrer las tres avenidas debe informar la cantidad total de papeles juntados.

   **Nota:** SE DEBE USAR MODULARIZACION (como mínimo debe haber un módulo para las calles, y otro para las avenidas). SEGURO QUE CADA CALLE TIENE AL MENOS 10 FLORES.

## Código relacionado

El repositorio incluye tres soluciones para la actividad adicional: [ejercicio 1](codigo/ejercicio-01.ri), [ejercicio 2](codigo/ejercicio-02.ri) y [ejercicio 3](codigo/ejercicio-03.ri).
