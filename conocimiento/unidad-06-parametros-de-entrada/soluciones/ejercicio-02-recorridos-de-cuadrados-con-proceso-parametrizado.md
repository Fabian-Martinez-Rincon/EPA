---
id: "EPA-U06-EJ02-SOLUCION"
titulo: "Solución: recorridos de la figura 6.5 reutilizando el proceso cuadrado"
slug: "ejercicio-02-recorridos-de-cuadrados-con-proceso-parametrizado"
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
  - "../ejercicios/ejercicio-02-recorridos-de-cuadrados-con-proceso-parametrizado.md"
  - "../soluciones/ejercicio-01-cuadrado-con-lado-como-parametro.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_2B"
  - "../codigo/soluciones/capitulo-06/Cap6_Preg_2C"
---

# Solución: recorridos de la figura 6.5 reutilizando el proceso cuadrado

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-02-recorridos-de-cuadrados-con-proceso-parametrizado.md`](../ejercicios/ejercicio-02-recorridos-de-cuadrados-con-proceso-parametrizado.md).

## Análisis

La clave de este ejercicio es que un cuadrado, al estar hecho con `repetir 4 { avanzar; derecha }`, siempre termina en la misma esquina donde empezó y con la misma orientación. Eso permite dos estrategias distintas para encadenar cuadrados de tamaño creciente sin volver a escribir el trazado:

- **Recorrido a) — variante B:** si después de cada `cuadrado(ancho)` no se reposiciona al robot, el siguiente cuadrado arranca exactamente donde arrancó el anterior. Llamando a `cuadrado` con `ancho` creciente (1, 2, 3, 4) sin mover al robot entre llamadas se obtienen varios cuadrados compartiendo el origen (1,1), como pide la figura 6.5 a).
- **Recorrido b) — variante C:** si en cambio se reposiciona al robot con `Pos(PosAv+ancho,1)` entre cada llamada, el siguiente cuadrado arranca `ancho` avenidas más allá del anterior — exactamente el ancho del cuadrado recién dibujado — formando una hilera de cuadrados crecientes apoyados unos junto a otros sobre la calle 1, como en la figura 6.5 b).

En ambos casos el parámetro de entrada `lado` del proceso `cuadrado` (ejercicio 1) es el único punto de contacto entre el programa principal y el proceso: la variable `ancho` del robot se copia en `lado` en cada invocación, sin que el proceso necesite saber nada de cómo se genera esa secuencia de tamaños.

## Estrategia

**Variante B (recorrido a):**

1. Inicializar `ancho := 1`.
2. Repetir 4 veces: invocar `cuadrado(ancho)` y luego incrementar `ancho` en 1, sin reposicionar al robot.

**Variante C (recorrido b):**

1. Inicializar `ancho := 1`.
2. Repetir 5 veces: invocar `cuadrado(ancho)`, reposicionar con `Pos(PosAv+ancho, 1)` para saltar al inicio del próximo cuadrado, e incrementar `ancho` en 1.

## Código relacionado

### Variante B — recorrido a) de la figura 6.5

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
    ancho:=1
    repetir 4
      cuadrado(ancho)
      ancho:=ancho+1
  fin
variables
  robin: robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-06/Cap6_Preg_2B`](../codigo/soluciones/capitulo-06/Cap6_Preg_2B)

### Variante C — recorrido b) de la figura 6.5

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
    ancho:=1
    repetir 5
      cuadrado(ancho)
      Pos(PosAv+ancho,1)
      ancho:=ancho+1  
  fin
variables
  robin: robot1
comenzar
  AsignarArea(robin,ciudad)
  Iniciar(robin,1,1)
fin
```

Código completo: [`../codigo/soluciones/capitulo-06/Cap6_Preg_2C`](../codigo/soluciones/capitulo-06/Cap6_Preg_2C)

## Nota sobre las variantes disponibles

El material histórico solo conserva las variantes "B" y "C" para este ejercicio (no existe una "variante A" separada); todo indica que el proceso `cuadrado` en sí — sin la lógica de encadenado — se cuenta como la solución del ejercicio 1, y B/C son las dos formas de encadenarlo pedidas por la figura 6.5. Ambas reutilizan el mismo proceso `cuadrado(E lado:numero)` sin modificarlo, tal como pide el enunciado.

## Escenario de prueba

No requiere flores ni papeles precargados, solo observar el recorrido. Conviene visualizar ambas variantes por separado: la B superpone cuadrados crecientes desde (1,1); la C los apoya en fila sobre la calle 1.

## Casos límite

- Primer cuadrado (`ancho = 1`): en ambas variantes es un cuadrado de una sola cuadra de lado.
- Variante C, último salto: tras el quinto `cuadrado(ancho)` el código igual ejecuta `Pos(PosAv+ancho,1)` y `ancho:=ancho+1`, aunque no haya un sexto cuadrado que dibujar; no tiene efecto visible, pero dejan al robot y a `ancho` en un estado que no vuelve a usarse.

## Errores frecuentes

- Reposicionar al robot en la variante B (rompería el patrón de "todos comparten origen") o no reposicionarlo en la variante C (los cuadrados quedarían superpuestos en vez de en hilera).
- Calcular mal el desplazamiento entre cuadrados en la variante C: tiene que ser exactamente `ancho` (el lado del cuadrado recién dibujado), no un valor fijo, para que no queden huecos ni superposiciones.

## Complejidad

Cada variante dibuja una cantidad fija de cuadrados (4 en B, 5 en C) de lados 1..4 o 1..5: O(n²) pasos totales en función de la cantidad de cuadrados, ya que el perímetro de cada uno crece linealmente con su lado.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-02-recorridos-de-cuadrados-con-proceso-parametrizado.md`](../ejercicios/ejercicio-02-recorridos-de-cuadrados-con-proceso-parametrizado.md)
- Código: [`../codigo/soluciones/capitulo-06/Cap6_Preg_2B`](../codigo/soluciones/capitulo-06/Cap6_Preg_2B), [`../codigo/soluciones/capitulo-06/Cap6_Preg_2C`](../codigo/soluciones/capitulo-06/Cap6_Preg_2C)
- Proceso base: [ejercicio 1](../ejercicios/ejercicio-01-cuadrado-con-lado-como-parametro.md)
