---
id: "EPA-U06-EJ01-SOLUCION"
titulo: "Solución: cuadrado con la longitud del lado como parámetro"
slug: "ejercicio-01-cuadrado-con-lado-como-parametro"
tipo: "solucion"
unidad: 6
tema: "parametros-de-entrada"
subtemas:
  - "declaracion-de-parametros"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 6-Parametros de Entrada.pdf"
    paginas: "1-20"
relacionados:
  - "../ejercicios/ejercicio-01-cuadrado-con-lado-como-parametro.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_1"
---

# Solución: cuadrado con la longitud del lado como parámetro

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-01-cuadrado-con-lado-como-parametro.md`](../ejercicios/ejercicio-01-cuadrado-con-lado-como-parametro.md).

## Análisis

Un cuadrado se traza avanzando `lado` cuadras y girando 90° (`derecha`), repetido 4 veces; como `derecha` gira en sentido horario, ese es exactamente el "sentido de las agujas del reloj" que pide el enunciado, sin importar la orientación inicial del robot (la regla de giro es relativa, no depende de si al entrar el robot mira hacia avenidas o calles crecientes). El proceso recibe `lado` como parámetro de entrada (`E`): el módulo que lo llama decide el tamaño, y el proceso solo lo lee para controlar el `repetir` interno, sin necesidad de modificarlo ni de devolver nada.

## Estrategia

1. Declarar `proceso cuadrado(E lado:numero)` con un único parámetro de entrada.
2. Repetir 4 veces: avanzar `lado` cuadras y girar a la derecha.
3. Desde el programa principal, invocar `cuadrado(ancho)` con el valor deseado; el robot queda de nuevo en la esquina de partida al terminar, porque un cuadrado siempre cierra sobre sí mismo.

## Código relacionado

```
programa  parametros
procesos
  proceso cuadrado(E lado:numero)
  comenzar
    repetir 4
      repetir lado
        mover
      derecha
  fin
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  variables
    ancho:numero
  comenzar
    ancho:=10
    cuadrado(ancho)
  fin
variables
  robin: robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-06/Cap6_Preg_1`](../codigo/soluciones/capitulo-06/Cap6_Preg_1)

## Escenario de prueba

No requiere flores ni papeles precargados: el ejercicio solo pide trazar el recorrido. Con la ciudad vacía alcanza para verificar que el robot dibuja un cuadrado de lado 10 a partir de (1,1) y vuelve a su esquina de origen.

## Casos límite

- `lado = 1`: el proceso sigue funcionando igual, dibujando el cuadrado mínimo (4 cuadras en total).
- Si `ancho` fuera lo bastante grande como para sacar al robot del área declarada (`AreaC(1,1,100,100)`), el intérprete cortaría la ejecución con un error de límites; con `ancho:=10` partiendo de (1,1) el cuadrado llega como máximo a la esquina (11,11), dentro del área.

## Errores frecuentes

- Declarar `lado` como variable local en vez de parámetro de entrada, lo que obligaría a tener un proceso distinto por cada tamaño de cuadrado (el problema que este mismo ejercicio busca evitar, ver sección 6.3 del capítulo).
- Usar `izquierda` en vez de `derecha`, invirtiendo el sentido de giro pedido por el enunciado.

## Complejidad

El recorrido tiene `4 × lado` pasos: O(lado) respecto del parámetro recibido.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-01-cuadrado-con-lado-como-parametro.md`](../ejercicios/ejercicio-01-cuadrado-con-lado-como-parametro.md)
- Código: [`../codigo/soluciones/capitulo-06/Cap6_Preg_1`](../codigo/soluciones/capitulo-06/Cap6_Preg_1)
