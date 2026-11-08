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

Recorrer "una calle" significa moverse manteniendo la calle fija y la avenida variable; como el robot arranca sin girar, hace falta un único `derecha` para que `mover` pase a incrementar `PosAv` en vez de `PosCa`. El proceso `JuntarFlor(E calle:numero; E NumFlores:numero)` reposiciona con `Pos(PosAv,calle)` (conserva la avenida actual, fija la calle pedida), gira, y recorre la calle avenida por avenida: en cada esquina levanta **todas** las flores que haya ahí (`mientras HayFlorEnLaEsquina`) antes de avanzar, y se detiene en cuanto junta la cantidad pedida (`CantFlores<NumFlores`) o llega al borde de la ciudad (`PosAv<100`, una condición de seguridad que en la práctica no debería activarse porque el enunciado garantiza que la cantidad pedida existe en el camino).

Los dos parámetros de entrada (`calle`, `NumFlores`) se usan exactamente como el capítulo indica que deben usarse: solo se leen, nunca se les asigna un valor dentro del proceso (la cuenta de flores recogidas se acumula en `CantFlores`, una variable local propia del proceso).

## Estrategia

1. Declarar `proceso JuntarFlor(E calle:numero; E NumFlores:numero)` con una variable local `CantFlores` inicializada implícitamente en 0.
2. Reposicionar con `Pos(PosAv,calle)` y girar a la derecha para orientarse a lo largo de la calle.
3. Mientras no se llegue al borde de la ciudad y falten flores por juntar: levantar todas las flores de la esquina actual y avanzar.

## Código relacionado

```rinfo
programa  parametros
procesos
  proceso izquierda
  comenzar
    repetir 2
      derecha
  fin
  proceso JuntarFlor(E calle:numero;E NumFlores:numero)
  variables
    CantFlores:numero
  comenzar
    Pos(PosAv,calle)
    derecha
    mientras(PosAv<100)&(CantFlores<NumFlores)
      mientras(HayFlorEnLaEsquina)
        tomarFlor
        CantFlores:=CantFlores+1
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
    JuntarFlor(callejon,NFlores)
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

Sembrá flores en la calle 19, sobre la avenida 1 y las que siguen: ahí es donde camina el robot. El programa arranca en (1,1), salta a (1,19) y avanza hacia el este. Con 4 flores repartidas en esas esquinas el proceso completa la cuenta y se frena.

## Casos límite

- Una esquina puede tener varias flores. El `mientras(HayFlorEnLaEsquina)` las levanta todas antes de avanzar, así que la cuenta puede saltar de 1 a 4 en una sola esquina.
- El `mover` de la última vuelta se ejecuta igual después de levantar la cuarta flor. El robot queda una avenida más adelante de donde la juntó.
- En la avenida 100 ya no levanta nada. La condición `PosAv<100` corta el `mientras` antes de revisar esa esquina.

## Errores frecuentes

- Usar `si(HayFlorEnLaEsquina)` en vez de `mientras`. El robot levanta una sola flor por esquina y puede terminar la calle sin completar la cuenta.
- Olvidar el `derecha` inicial. El robot sube por la avenida 1 en vez de recorrer la calle 19 hacia la derecha.

## Complejidad

En el peor caso recorre hasta 99 esquinas de la calle indicada (todo el ancho de la ciudad): O(n) respecto del tamaño de la ciudad, acotado por la garantía del enunciado de que las flores pedidas existen antes de llegar al final.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-07-juntar-flores-en-una-calle-parametrizada.md`](../ejercicios/ejercicio-07-juntar-flores-en-una-calle-parametrizada.md)
- Código: [`../codigo/soluciones/capitulo-06/Cap6_Preg_7`](../codigo/soluciones/capitulo-06/Cap6_Preg_7)
