---
id: "EPA-U05-EJ01-ENUNCIADO"
titulo: "Ejercicio 1: proceso cuadrado de lado 2 en sentido horario"
slug: "ejercicio-01-cuadrado-lado-2-horario"
tipo: "ejercicio"
unidad: 5
tema: "programacion-estructurada"
subtemas:
  - "programacion-modular"
  - "procesos-sin-parametros"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 5-Programacion Estructurada.pdf"
    paginas: "1-24"
prerrequisitos:
  - "../capitulo-5-programacion-estructurada.md"
relacionados:
  - "../soluciones/ejercicio-01-cuadrado-lado-2-horario.md"
  - "../ejercicios/ejercicio-02-recorridos-con-cuadrado.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-05/Cap5_1"
---

# Ejercicio 1: proceso cuadrado de lado 2 en sentido horario

## Enunciado

Escriba un proceso que le permita al robot realizar un cuadrado de lado 2 girando en la dirección de las agujas del reloj.

## Datos

- **Entradas:** ninguna leída en tiempo de ejecución; el proceso se invoca desde la esquina donde esté parado el robot al momento de la llamada.
- **Salidas:** ninguna; el resultado se observa en el recorrido trazado por el robot (un cuadrado de 2x2 esquinas).
- **Restricciones:** el giro debe hacerse en sentido horario (usando la primitiva `derecha`, que gira 90° en sentido horario).

## Referencias

- Solución: [`../soluciones/ejercicio-01-cuadrado-lado-2-horario.md`](../soluciones/ejercicio-01-cuadrado-lado-2-horario.md)
- Código: [`../codigo/soluciones/capitulo-05/Cap5_1`](<../codigo/soluciones/capitulo-05/Cap5_1>)
- Relacionado: el proceso `cuadrado` de este ejercicio se reutiliza en el [ejercicio 2](ejercicio-02-recorridos-con-cuadrado.md).
