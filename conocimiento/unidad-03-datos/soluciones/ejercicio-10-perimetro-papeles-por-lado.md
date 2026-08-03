---
id: "EPA-U03-EJ10-SOLUCION"
titulo: "Solución: recorrer el perímetro informando los papeles recogidos por lado"
slug: "ejercicio-10-perimetro-papeles-por-lado"
tipo: "solucion"
unidad: 3
tema: "datos-y-variables"
subtemas:
  - "variables"
  - "estructuras-de-control"
  - "primitivas-del-robot"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 3-Datos.pdf"
    paginas: "1-21"
relacionados:
  - "../ejercicios/ejercicio-10-perimetro-papeles-por-lado.md"
codigo_relacionado:
  - "../codigo/capitulo-3-pregunta-10.ri"
escenario_ciudad:
  - av: 1
    ca: 30
    papeles: 2
  - av: 60
    ca: 100
    papeles: 3
  - av: 100
    ca: 40
    papeles: 5
  - av: 20
    ca: 1
    papeles: 1
---

# Solución: recorrer el perímetro informando los papeles recogidos por lado

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-10-perimetro-papeles-por-lado.md`](../ejercicios/ejercicio-10-perimetro-papeles-por-lado.md).

## Análisis

Se repite cuatro veces (una por lado) el mismo patrón usado para recorrer una avenida o calle completa: `repetir 99 {tomar todos los papeles; mover} + procesar la última esquina del lado`, acumulando en una variable distinta por lado (`lado1`...`lado4`), y un `derecha` entre lado y lado para girar en el vértice. Es el mismo patrón, ya verificado, de `ejercicio-11` de la unidad 2 (recorrido de todo el perímetro), aplicado acá para contar papeles en vez de depositarlos.

## Estrategia

1. Inicializar los cuatro contadores en 0.
2. Repetir cuatro veces: recorrer 99 esquinas de un lado tomando papeles y contándolos en el contador de ese lado, procesar la última esquina del lado (el vértice), y girar a la derecha (salvo que ya se completaron los cuatro lados).
3. Informar los cuatro contadores.

## Código relacionado

```
programa prueba
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  variables
    lado1: numero
    lado2: numero
    lado3: numero
    lado4: numero
  comenzar
    lado1:=0
    lado2:=0
    lado3:=0
    lado4:=0
    repetir 99
      mientras(HayPapelEnLaEsquina)
        tomarPapel
        lado1:=lado1+1
      mover
    mientras(HayPapelEnLaEsquina)
      tomarPapel
      lado1:=lado1+1
    derecha
    repetir 99
      mientras(HayPapelEnLaEsquina)
        tomarPapel
        lado2:=lado2+1
      mover
    mientras (HayPapelEnLaEsquina)
      tomarPapel
      lado2:=lado2+1
    derecha
    repetir 99
      mientras HayPapelEnLaEsquina
        tomarPapel
        lado3:=lado3+1
      mover
    mientras HayPapelEnLaEsquina
      tomarPapel
      lado3:=lado3+1
    derecha
    repetir 99
      mientras(HayPapelEnLaEsquina)
        tomarPapel
        lado4:=lado4+1
      mover
    mientras(HayPapelEnLaEsquina)
      tomarPapel
      lado4:=lado4+1
    Informar(lado1,lado2,lado3,lado4)
  fin
variables
  robin:robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/capitulo-3-pregunta-10.ri`](../codigo/capitulo-3-pregunta-10.ri)

## Escenario de prueba

Cargar papeles en una esquina de cada uno de los cuatro lados del perímetro (por ejemplo, (1,30) con 2 papeles para el lado 1, (60,100) con 3 para el lado 2, (100,40) con 5 para el lado 3 y (20,1) con 1 para el lado 4). Probado con el intérprete: el programa informa exactamente `(2,3,5,1)`, cada cantidad atribuida al lado correcto.

## Casos límite

- Un vértice compartido entre dos lados sólo se cuenta una vez, del lado que termina en él: el lado siguiente vuelve a chequear ese mismo vértice, pero ya está vacío (mismo comportamiento verificado en `ejercicio-11` de la unidad 2).
- Perímetro completamente vacío: los cuatro contadores terminan en 0.

## Errores frecuentes

- Olvidar el `derecha` entre lado y lado, lo que haría que el robot siguiera de largo en la misma dirección en vez de girar en el vértice.
- Reutilizar la misma variable para los cuatro lados en vez de una por lado, perdiendo la separación de las cuentas.

## Complejidad

Perímetro fijo de 4×99 esquinas: O(1) respecto al tamaño de la ciudad (perímetro fijo en 100×100).

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-10-perimetro-papeles-por-lado.md`](../ejercicios/ejercicio-10-perimetro-papeles-por-lado.md)
- Fuente original: [`../fuentes/Capitulo 3-Datos.pdf`](<../fuentes/Capitulo 3-Datos.pdf>)
- Código: [`../codigo/capitulo-3-pregunta-10.ri`](../codigo/capitulo-3-pregunta-10.ri)
