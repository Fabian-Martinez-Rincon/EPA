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

```rinfo
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

El robot arranca en (1,1) mirando al norte, así que los lados salen en este orden: el 1 sube por la avenida 1, el 2 va por la calle 100, el 3 baja por la avenida 100 y el 4 vuelve por la calle 1.

Cargá papeles en un lado cada uno: 2 en (1,30), 3 en (60,100), 5 en (100,40) y 1 en (20,1). El robot informa `(2,3,5,1)`, cada cantidad en el contador que le toca.

## Casos límite

- Perímetro vacío: informa `(0,0,0,0)`.
- Cada vértice lo cuenta un solo lado, el primero que pasa por ahí: se lleva los papeles y el siguiente encuentra la esquina vacía. Con un papel en cada uno de los cuatro vértices el robot informa `(2,1,1,0)`. El lado 1 se lleva dos, el de arranque (1,1) y el (1,100) donde termina, y al lado 4 no le queda ninguno.

## Errores frecuentes

- Olvidar un `derecha` en un vértice. El robot intenta seguir derecho, se sale de la ciudad y el programa corta con error.
- Usar un solo contador para los cuatro lados. El total de papeles del perímetro te va a dar bien, pero el enunciado pide el desglose lado por lado.

## Complejidad

Perímetro fijo de 4×99 esquinas: O(1) respecto al tamaño de la ciudad (perímetro fijo en 100×100).

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-10-perimetro-papeles-por-lado.md`](../ejercicios/ejercicio-10-perimetro-papeles-por-lado.md)
- Código: [`../codigo/capitulo-3-pregunta-10.ri`](../codigo/capitulo-3-pregunta-10.ri)
