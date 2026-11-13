---
id: "EPA-U06-EJ07-SOLUCION"
titulo: "Solución: juntar una cantidad de flores en una calle parametrizada"
slug: "ejercicio-07-juntar-flores-en-una-calle-parametrizada"
tipo: "solucion"
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
relacionados:
  - "../ejercicios/ejercicio-07-juntar-flores-en-una-calle-parametrizada.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_7"
escenario_ciudad:
  - av: 1
    ca: 19
    flores: 2
  - av: 2
    ca: 19
    flores: 2
---

# Solución: juntar una cantidad de flores en una calle parametrizada

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-07-juntar-flores-en-una-calle-parametrizada.md`](../ejercicios/ejercicio-07-juntar-flores-en-una-calle-parametrizada.md).

## Análisis

Recorrer una calle es moverse con la calle fija y la avenida variable. El robot arranca mirando al norte, así que hace falta un `derecha` para que `mover` lo lleve hacia el este, por la calle.

El proceso `CalleFlor(E calle:numero; E NumFlores:numero)` ubica al robot en la calle pedida con `Pos(PosAv,calle)`, gira y cuenta las flores que junta en una variable local, `CantFlores`, que arranca en 0. En cada vuelta toma **una** flor si hay, o avanza si la esquina está vacía. Así una esquina con muchas flores se va vaciando de a una, y el ciclo corta justo cuando la cuenta llega a `NumFlores`, sin levantar ni una de más. Como el enunciado garantiza que esas flores existen, no hace falta preguntar por el borde de la ciudad.

Los dos parámetros de entrada solo se leen: la cuenta se lleva en `CantFlores`, no en `NumFlores`.

## Estrategia

1. Declarar `proceso CalleFlor(E calle:numero; E NumFlores:numero)` con la variable local `CantFlores`, y ponerla en 0.
2. Ubicar al robot con `Pos(PosAv,calle)` y girar a la derecha.
3. Mientras `CantFlores<NumFlores`: si hay flor, tomarla y sumar 1; si no, avanzar.

## Código relacionado

```rinfo
programa  parametros
procesos
  proceso CalleFlor(E calle:numero;E NumFlores:numero)
  variables
    CantFlores:numero
  comenzar
    CantFlores:=0
    Pos(PosAv,calle)
    derecha
    mientras(CantFlores<NumFlores)
      si(HayFlorEnLaEsquina)
        tomarFlor
        CantFlores:=CantFlores+1
      sino
        mover
  fin
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  variables
    callejon:numero
    NFlores:numero
  comenzar
    NFlores:=4
    callejon:=19
    CalleFlor(callejon,NFlores)
  fin
variables
  robin: robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-06/Cap6_Preg_7`](../codigo/soluciones/capitulo-06/Cap6_Preg_7)

## Escenario de prueba

Con una flor en (3,19), dos en (6,19), una en (10,19) y tres en (15,19), el robot junta las 4 que pide el programa y se queda en (10,19), donde tomó la cuarta. Las tres de la avenida 15 quedan donde estaban.

## Casos límite

- Una esquina con más flores de las que faltan: el robot toma solo las que necesita y deja el resto. Con 7 flores en (4,19), junta 4 y deja 3.
- El robot termina parado en la esquina donde tomó la última flor, no una más adelante: cuando la cuenta se completa, el ciclo corta antes del próximo `mover`.

## Errores frecuentes

- No poner `CantFlores:=0`. Inicializar el contador es parte del algoritmo: no dependas del valor con el que el ambiente crea la variable. Si la cuenta no arranca en 0, el robot junta de menos o de más.
- Vaciar la esquina con `mientras(HayFlorEnLaEsquina)` adentro del ciclo. Si la esquina tiene más flores de las que faltan, el robot las levanta todas y se pasa de lo pedido.
- Olvidar el `derecha` inicial. El robot sube por la avenida 1 en vez de recorrer la calle 19.

## Complejidad

En el peor caso recorre la calle entera: O(n) respecto del ancho de la ciudad, más una vuelta por cada flor que toma.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-07-juntar-flores-en-una-calle-parametrizada.md`](../ejercicios/ejercicio-07-juntar-flores-en-una-calle-parametrizada.md)
- Código: [`../codigo/soluciones/capitulo-06/Cap6_Preg_7`](../codigo/soluciones/capitulo-06/Cap6_Preg_7)
