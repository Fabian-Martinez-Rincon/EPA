---
id: "EPA-U03-EJ08-SOLUCION"
titulo: "Solución: caminar la calle 2 hasta encontrar al menos 10 papeles"
slug: "ejercicio-08-diez-papeles-calle-2-al-menos"
tipo: "solucion"
unidad: 3
tema: "datos-y-variables"
subtemas:
  - "variables"
  - "estructuras-de-control"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 3-Datos.pdf"
    paginas: "1-21"
relacionados:
  - "../ejercicios/ejercicio-08-diez-papeles-calle-2-al-menos.md"
codigo_relacionado:
  - "../codigo/capitulo-3-pregunta-08.ri"
escenario_ciudad:
  - av: 3
    ca: 2
    papeles: 1
  - av: 4
    ca: 2
    papeles: 1
  - av: 5
    ca: 2
    papeles: 1
  - av: 6
    ca: 2
    papeles: 1
  - av: 7
    ca: 2
    papeles: 1
  - av: 8
    ca: 2
    papeles: 1
  - av: 9
    ca: 2
    papeles: 1
  - av: 10
    ca: 2
    papeles: 1
  - av: 11
    ca: 2
    papeles: 1
  - av: 12
    ca: 2
    papeles: 1
---

# Solución: caminar la calle 2 hasta encontrar al menos 10 papeles

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-08-diez-papeles-calle-2-al-menos.md`](../ejercicios/ejercicio-08-diez-papeles-calle-2-al-menos.md).

## Análisis

Como no se garantiza que existan 10 papeles, el recorrido tiene dos formas de terminar: juntar 10 (`x<10` deja de cumplirse) o llegar al final de la calle (`PosAv<100` deja de cumplirse). Las dos condiciones van juntas en el `mientras`, unidas con `&`. En cada esquina se juntan todos los papeles que haya, por eso el robot puede terminar con más de 10: el enunciado pide "al menos" 10.

## Estrategia

1. Posicionar el robot en (1,2) y girar a la derecha.
2. Mientras `x<10` y `PosAv<100`: juntar todos los papeles de la esquina contándolos en `x`, y avanzar solo si todavía faltan papeles. Así el robot se queda parado en la esquina donde completó los 10.
3. Si al llegar a la avenida 100 todavía faltan, revisar esa última esquina, que el `mientras` no llega a mirar.
4. Informar la posición final.

## Código relacionado

```rinfo
programa prueba
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  variables
    x: numero
    y: numero
  comenzar
    Pos(1,2)
    x:=0
    derecha
    mientras((x<10) & (PosAv<100))
      mientras(HayPapelEnLaEsquina)
        tomarPapel
        x:=x+1
      si(x<10)
        mover
    si(x<10)
      mientras(HayPapelEnLaEsquina)
        tomarPapel
        x:=x+1
    Informar(PosAv,PosCa)
  fin
variables
  robin:robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/capitulo-3-pregunta-08.ri`](../codigo/capitulo-3-pregunta-08.ri)

## Escenario de prueba

Poné 10 papeles en la calle 2, uno por esquina, en las avenidas 3 a 12. El robot junta el décimo en la avenida 12, se queda ahí e informa `(12,2)`. Probá después sin ningún papel: recorre la calle entera e informa `(100,2)`.

## Casos límite

- Sin papeles en la calle, o con menos de 10: el robot la recorre entera e informa `(100,2)`.
- Si la décima parte cae justo en la avenida 100, la junta el bloque que va después del `mientras`. Ese bloque está para eso: el `mientras` frena con `PosAv` en 100 antes de mirar esa esquina.
- Una esquina con varios papeles se vacía entera aunque se pase de 10. Por eso el enunciado dice "al menos".

## Errores frecuentes

- Poner el `mover` sin el `si(x<10)`. El robot completa los 10 y da un paso más antes de que el `mientras` corte, así que informa la esquina siguiente a la del décimo papel.
- Controlar solo `PosAv<100`. El robot junta los 10 y sigue caminando hasta el final de la calle: siempre informa `(100,2)`.
- Controlar solo `x<10`. Si no hay 10 papeles, el robot sale de la ciudad por la avenida 101.

## Complejidad

Recorrido de hasta 100 esquinas (una calle completa): O(1) respecto al tamaño de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-08-diez-papeles-calle-2-al-menos.md`](../ejercicios/ejercicio-08-diez-papeles-calle-2-al-menos.md)
- Código: [`../codigo/capitulo-3-pregunta-08.ri`](../codigo/capitulo-3-pregunta-08.ri)
