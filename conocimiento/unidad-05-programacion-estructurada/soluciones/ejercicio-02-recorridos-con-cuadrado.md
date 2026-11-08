---
id: "EPA-U05-EJ02-SOLUCION"
titulo: "Solución: recorridos de la figura 5.9 usando el proceso cuadrado"
slug: "ejercicio-02-recorridos-con-cuadrado"
tipo: "solucion"
unidad: 5
tema: "programacion-estructurada"
subtemas:
  - "programacion-modular"
  - "reusabilidad-de-procesos"
nivel: "inicial"
lenguajes:
  - "R-info"
estado: "completo"
origen: "convertido"
fuentes:
  - archivo: "../fuentes/Capitulo 5-Programacion Estructurada.pdf"
    paginas: "1-24"
relacionados:
  - "../ejercicios/ejercicio-02-recorridos-con-cuadrado.md"
  - "../soluciones/ejercicio-01-cuadrado-lado-2-horario.md"
codigo_relacionado:
  - "../codigo/soluciones/capitulo-05/Cap5_2A"
  - "../codigo/soluciones/capitulo-05/Cap5_2B"
---

# Solución: recorridos de la figura 5.9 usando el proceso cuadrado

## Enunciado relacionado

Ver [`../ejercicios/ejercicio-02-recorridos-con-cuadrado.md`](../ejercicios/ejercicio-02-recorridos-con-cuadrado.md).

## Análisis

Ambas variantes reutilizan el proceso `cuadrado` del ejercicio 1 (ya corregido a lado 2) e implementan un segundo proceso que invoca `cuadrado` varias veces, reposicionando al robot con `Pos` entre una invocación y la siguiente. Como `cuadrado` es una "caja negra" que siempre deja al robot en la misma esquina y orientación en que fue invocado (propiedad explicada en el Ejemplo 5.6 de la teoría), el proceso que arma el recorrido completo no necesita preocuparse por cómo se dibuja cada cuadrado individual: solo por dónde ubicarlo.

- **Variante A** (proceso `A`), corresponde al recorrido **a)** de la figura 5.9: `repetir 3: cuadrado; Pos(PosAv+3,PosCa+3)`. Traza tres cuadrados de lado 2 en diagonal ascendente, cada uno separado del anterior por una esquina de margen (con lado 2, un cuadrado que arranca en (1,1) ocupa hasta (3,3); el siguiente arranca recién en (4,4), tocando al anterior por una única esquina). Este mismo patrón —módulo de figura + `Pos` que avanza exactamente lado+1— es el que usa la propia teoría del capítulo en la "solución 2" del Ejemplo 5.6 para separar tres cuadrados sin que se toquen, generalizado acá de un desplazamiento horizontal a uno diagonal.
- **Variante B** (proceso `B`, en el mismo archivo que también conserva sin usar el proceso `A`), corresponde al recorrido **b)** de la figura 5.9: `repetir 2: cuadrado; Pos(1,PosCa+5)`. Traza dos cuadrados, ambos arrancando en la avenida 1 (`PosAv` no cambia entre invocaciones), con las calles de partida separadas por 5 — un apilamiento vertical en la misma columna, no un desplazamiento diagonal.

## Estrategia

1. Declarar el proceso `cuadrado` del ejercicio 1 (sin modificarlo).
2. Declarar un proceso adicional que invoque `cuadrado` la cantidad de veces necesaria, reposicionando al robot con `Pos` (coordenadas absolutas, no relativas a la orientación) entre cada invocación.
3. Invocar ese proceso adicional una única vez desde el cuerpo del robot.

## Código relacionado

**Variante A:**

```rinfo
proceso cuadrado
comenzar
  repetir 4
    repetir 2
      mover
    derecha
fin
proceso A
comenzar
  repetir 3
    cuadrado
    Pos(PosAv+3,PosCa+3)
fin
```

Código completo: [`../codigo/soluciones/capitulo-05/Cap5_2A`](<../codigo/soluciones/capitulo-05/Cap5_2A>)

**Variante B:**

```rinfo
proceso B
comenzar
  repetir 2
    cuadrado
    Pos(1,PosCa+5)
fin
```

Código completo: [`../codigo/soluciones/capitulo-05/Cap5_2B`](<../codigo/soluciones/capitulo-05/Cap5_2B>)

## Corrección aplicada: bug de `cuadrado` heredado del ejercicio 1

Igual que en el ejercicio 1 (del que ambos archivos heredan una copia del proceso `cuadrado`): el `repetir 3` interno de `cuadrado` se corrigió a `repetir 2` en los dos archivos, por la misma evidencia (enunciado, comentario del archivo y Ejemplo 5.6 de la teoría). Ver el detalle en la solución del [ejercicio 1](ejercicio-01-cuadrado-lado-2-horario.md).

## Corrección aplicada: correspondencia con las figuras a) y b) confirmada

El archivo `Cap5_2B` conserva, sin usar, una copia completa del proceso `A` (además de `B`, que es el que efectivamente se invoca) — es decir, ambas variantes de recorrido conviven en el mismo archivo histórico, y solo una se ejecuta en cada uno. Esto es consistente con que el enunciado pide "un programa para cada uno" de los dos recorridos de la figura 5.9, resueltos acá como dos programas (A y B) que comparten el mismo módulo base `cuadrado`.

Originalmente no se había podido confirmar, a simple vista sobre la figura escaneada de baja resolución, cuál de las dos variantes correspondía a cada recorrido. Se resolvió recortando y ampliando (4x, interpolación por vecino más cercano) cada mitad de `figura-5-9-recorridos-cuadrados.png` y comparándola contra la traza real del intérprete (eventos `pos` — los saltos `Pos(...)` entre cuadrados):

- **Recorrido a)**: la figura muestra tres cuadrados en una escalera diagonal, cada uno tocando al siguiente por una sola esquina. La variante A, corrida contra el intérprete, invoca `cuadrado` en (1,1), (4,4) y (7,7) — un desplazamiento diagonal de 3 en 3 (esquina de margen entre cuadrados de lado 2), que reproduce exactamente esa escalera. **A = a)**.
- **Recorrido b)**: la figura muestra dos cuadrados apilados **en la misma columna** (misma avenida), uno arriba del otro con un hueco entre ambos — no en diagonal, a diferencia de lo que sugería una lectura apresurada de la imagen original. La variante B, corrida contra el intérprete, invoca `cuadrado` en (1,1) y (1,6): misma avenida (1), calle desplazada en 5. **B = b)**.

Con esta verificación, la correspondencia queda confirmada con evidencia directa (imagen ampliada + traza del intérprete) en lugar de asumida; ver también la corrección de redacción aplicada en el propio enunciado del ejercicio 2, que originalmente describía b) como "en diagonal" por error.

## Escenario de prueba

Ciudad vacía en las dos variantes: ninguna junta ni deposita nada.

Mirá dónde arranca cada cuadrado. En la variante A el robot los dibuja en (1,1), (4,4) y (7,7). En la B, en (1,1) y (1,6). Es lo único que cambia entre una y otra.

## Casos límite

- Los saltos van con `Pos`, que recibe avenida y calle absolutas. No importa hacia dónde quedó mirando el robot al cerrar un cuadrado: el siguiente arranca donde diga el `Pos`.
- Las dos variantes hacen un `Pos` de más al final, después del último cuadrado. En la A el robot termina parado en (10,10) sin dibujar nada ahí.
- Si subís el `repetir 3` de la variante A, entra hasta 33. Con 34 el último cuadrado arranca en (100,100) y el `mover` se sale de la ciudad.

## Errores frecuentes

- Copiar el cuerpo del cuadrado adentro de `A` o `B` en vez de invocar `cuadrado`. El ejercicio es justamente reusar el proceso del ejercicio 1.
- Reposicionar con `mover` en vez de `Pos`. Te obliga a llevar la cuenta de hacia dónde mira el robot en cada momento, que es lo que `Pos` te ahorra.

## Complejidad

Cada variante traza una cantidad fija de cuadrados (3 en A, 2 en B): O(1) respecto al tamaño de la ciudad.

## Fuentes y archivos relacionados

- Enunciado: [`../ejercicios/ejercicio-02-recorridos-con-cuadrado.md`](../ejercicios/ejercicio-02-recorridos-con-cuadrado.md)
- Figura: [`../recursos/figura-5-9-recorridos-cuadrados.png`](<../recursos/figura-5-9-recorridos-cuadrados.png>)
- Código: [`../codigo/soluciones/capitulo-05/Cap5_2A`](<../codigo/soluciones/capitulo-05/Cap5_2A>), [`../codigo/soluciones/capitulo-05/Cap5_2B`](<../codigo/soluciones/capitulo-05/Cap5_2B>)
