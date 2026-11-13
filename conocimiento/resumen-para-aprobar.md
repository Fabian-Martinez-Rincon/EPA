---
id: "CON-EPA-RESUMEN-PARA-APROBAR"
titulo: "Resumen para aprobar el Curso de Ingreso"
slug: "resumen-para-aprobar"
tipo: "teoria"
tema: "resumen-integrador"
nivel: "inicial"
estado: "completo"
origen: "elaborado"
lenguajes:
  - "R-info"
relacionados:
  - "unidad-00-introduccion/capitulo-0-introduccion.md"
  - "unidad-01-resolucion-de-problemas/capitulo-1-resolucion-de-problemas.md"
  - "unidad-02-algoritmos-y-logica/capitulo-2-algoritmos-y-logica.md"
  - "unidad-03-datos/capitulo-3-datos.md"
  - "unidad-04-repaso/capitulo-4-repaso.md"
  - "unidad-05-programacion-estructurada/capitulo-5-programacion-estructurada.md"
  - "unidad-06-parametros-de-entrada/capitulo-6-parametros-de-entrada.md"
  - "unidad-07-parametros-de-entrada-salida/capitulo-7-parametros-de-entrada-salida.md"
---

# Resumen para aprobar el Curso de Ingreso

Este resumen junta en un solo lugar todo lo que se evalúa en el Curso de Ingreso (EPA): la teoría de los capítulos 1 a 7, cada instrucción del robot R-info, los patrones de código que aparecen en todos los exámenes y la lista de errores que más puntos hacen perder. Leelo entero una vez, y antes del examen repasá las secciones de patrones, errores y la lista final.

## Qué es un algoritmo

Un **algoritmo** es una secuencia ordenada de pasos elementales, sin ambigüedades, que resuelve un problema en un tiempo finito. De esa definición salen las tres propiedades que te pueden preguntar:

- **No es ambiguo.** Cada paso significa una sola cosa. "Ponerle algo de sal" es ambiguo; "agregarle una cucharadita de sal" no.
- **Termina.** "Sumar todos los números enteros" no tiene algoritmo, porque nunca termina.
- **Está hecho de pasos elementales.** Un paso elemental es uno que no se puede dividir en otros más simples. Qué es elemental depende de quién lo ejecuta: para una computadora el conjunto es muy chico, por eso los algoritmos llevan mucho detalle. A partir de acá, **instrucción** es sinónimo de paso elemental.

> La **precondición** es lo que se sabe verdadero antes de empezar. La **postcondición** es lo que se sabe verdadero al terminar, si el algoritmo hizo lo que se pedía.

Ejemplo: para volcar un montículo de arena en una zanja, la precondición es que tenés la pala, la arena y estás al lado de la zanja; la postcondición es que el montículo quedó vacío.

### Las etapas para resolver un problema con computadora

1. **Análisis del problema:** entender qué se pide y con qué datos se cuenta. En el curso, esto es interpretar bien el enunciado.
2. **Diseño de una solución:** dividir el problema en subproblemas (se trabaja a fondo en el capítulo 5).
3. **Especificación de algoritmos:** escribir los pasos de cada subproblema.
4. **Escritura del programa:** pasar el algoritmo a un lenguaje de programación. La **compilación** lo traduce al lenguaje de la máquina y detecta los errores de sintaxis.
5. **Verificación:** ejecutar con datos representativos y comprobar que el resultado es el correcto.

En cualquier etapa podés encontrar errores que te obligan a volver a una anterior.

## Las cuatro estructuras de control

El **flujo de control** es el orden en que se ejecutan las instrucciones. Las **estructuras de control** cambian ese orden. Son cuatro y tenés que saber reconocer cuál corresponde a cada situación:

| Estructura | En R-info | Cuándo se usa |
|---|---|---|
| Secuencia | una instrucción debajo de otra | siempre que no haya que decidir ni repetir |
| Selección | `si (condición)` … `sino` … | hay que elegir entre dos caminos según algo que solo se sabe al ejecutar |
| Repetición | `repetir N` | se repite una cantidad **conocida de antemano** |
| Iteración | `mientras (condición)` | se repite una cantidad **desconocida**, hasta que algo cambie |

Lo que más se pregunta de cada una:

- En la **selección**, se ejecuta una sola de las dos ramas, nunca las dos. El `sino` es opcional: sin él, si la condición es falsa no se hace nada.
- En la **repetición**, la cantidad tiene que conocerse antes de empezar. Puede ser un número (`repetir 99`) o una variable con un valor ya calculado (`repetir flores`). Con `repetir 0` el bloque no se ejecuta ninguna vez.
- En la **iteración**, la condición se evalúa **antes** de cada vuelta, también antes de la primera. Si de entrada es falsa, el bloque no se ejecuta nunca. Y adentro del bloque algo tiene que cambiar el valor de la condición, si no la iteración no termina.

> La **indentación** (sangría) es lo único que dice qué instrucciones pertenecen a una estructura. En R-info el cuerpo va dos columnas más a la derecha que la palabra que lo abre. Una instrucción con la misma sangría que el `si`, el `repetir` o el `mientras` ya no pertenece a esa estructura.

## La ciudad y el robot R-info

- La ciudad tiene **100 avenidas y 100 calles**. Las **avenidas son verticales** y las **calles horizontales**.
- Una esquina se escribe **(avenida, calle)**: primero la avenida. La esquina (2,4) es avenida 2 y calle 4.
- Las avenidas crecen de izquierda a derecha y las calles de abajo hacia arriba. (1,1) es la esquina de abajo a la izquierda.
- Un paso del robot es una cuadra. Las flores y los papeles están siempre en las esquinas, y puede haber varios en la misma.
- El robot arranca en (1,1) **mirando al norte** (hacia arriba). Solo puede girar **a la derecha**: no existe `izquierda`.
- Lleva una **bolsa** de capacidad ilimitada y toma o deja los objetos **de a uno**.

### Las instrucciones del robot

| Instrucción | Qué hace | Cuidado |
|---|---|---|
| `mover` | avanza una cuadra hacia donde mira | si se sale de la ciudad, el programa se corta con error |
| `derecha` | gira 90° en sentido horario | |
| `tomarFlor` / `tomarPapel` | levanta uno de la esquina y lo guarda en la bolsa | si la esquina no tiene, error |
| `depositarFlor` / `depositarPapel` | deja uno de la bolsa en la esquina | si la bolsa no tiene, error |
| `Pos(av, ca)` | salta a la esquina (av, ca) | **no** cambia la orientación |
| `Informar(...)` | muestra valores en pantalla | admite varios valores separados por coma |
| `PosAv` / `PosCa` | número de avenida / calle donde está parado | se pueden leer, **nunca** asignar |
| `HayFlorEnLaEsquina` / `HayPapelEnLaEsquina` | V si hay al menos uno en la esquina | dice si hay, no cuántos |
| `HayFlorEnLaBolsa` / `HayPapelEnLaBolsa` | V si hay al menos uno en la bolsa | |

> Que la instrucción no falle es **responsabilidad del programador**. Antes de `tomarFlor` preguntá `HayFlorEnLaEsquina`; antes de `depositarFlor` preguntá `HayFlorEnLaBolsa`; antes de `mover` asegurate de no estar en el borde. La única excepción es cuando el enunciado lo garantiza ("seguro tiene", "seguro existe").

`PosAv := 3` no compila: para ir a otra esquina se usa `Pos(3,4)`. Para contar flores no hay instrucción: hay que tomarlas de a una y contar (ver los patrones más abajo).

### Hacia dónde mira

Como solo gira a la derecha, para cada orientación hay una cantidad fija de `derecha` desde el norte:

| Para mirar al… | desde el norte hacés | sirve para recorrer… |
|---|---|---|
| Norte (arriba) | nada | una avenida, de la calle 1 a la 100 |
| Este (derecha) | `derecha` | una calle, de la avenida 1 a la 100 |
| Sur (abajo) | `repetir 2` `derecha` | una avenida hacia abajo |
| Oeste (izquierda) | `repetir 3` `derecha` | una calle hacia la izquierda |

Girar a la izquierda es `repetir 3` `derecha`.

## El esqueleto de todo programa

Este es el programa mínimo. En el curso **solo cambia lo que está entre el `comenzar` y el `fin` del robot** (y, más adelante, las variables del robot y la sección de procesos). El área, el robot y su arranque en (1,1) son siempre iguales.

```rinfo
programa Esqueleto
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  variables
    flores: numero
  comenzar
    {acá va lo que hace el robot}
    flores := 0
    mover
    Informar(flores)
  fin
variables
  R-info: robot1
comenzar
  AsignarArea(R-info,ciudad)
  Iniciar(R-info,1,1)
fin
```

El orden de las secciones es fijo: `programa`, `procesos` (si hay), `areas`, `robots`, `variables`, y el `comenzar … fin` del programa.

Reglas de escritura que se corrigen:

- **Mayúsculas y minúsculas importan.** `depositarFlor` es correcto; `DepositarFlor` y `depositarflor` no compilan.
- Las palabras clave, primitivas y estructuras van en minúscula, y si tienen varias palabras, de la segunda en adelante empiezan con mayúscula: `tomarFlor`, `mientras`, `numero`.
- Lo que provee el sistema empieza cada palabra con mayúscula: `PosAv`, `HayFlorEnLaBolsa`, `Pos`, `Informar`.
- La indentación es de **dos espacios** por nivel.
- Los **comentarios** van entre llaves: `{recorro la avenida 1}`. Son comentarios lógicos: dicen qué logra un bloque, no repiten la instrucción.

## Lógica: condiciones simples y compuestas

Una **proposición** es una expresión que puede ser verdadera o falsa (no las dos). "1 + 4 = 5" es una proposición; "un triángulo es menor que un círculo" no lo es.

- Es **atómica** si no tiene conectivos: `HayFlorEnLaEsquina`, `PosCa < 100`.
- Es **molecular** (compuesta) si une atómicas con conectivos.

| Conectivo | Símbolo en R-info | Es verdadera cuando… |
|---|---|---|
| y (conjunción) | `&` | las **dos** son verdaderas |
| o (disyunción) | `\|` | **al menos una** es verdadera (es un "o" incluyente) |
| no (negación) | `~` | la proposición es falsa |

| p | q | p & q | p \| q | ~p |
|---|---|---|---|---|
| V | V | V | V | F |
| V | F | F | V | F |
| F | V | F | V | V |
| F | F | F | F | V |

- La palabra **"pero"** funciona como un "y": "no hay flor en la bolsa, pero hay en la esquina" es `~p & q`.
- **Prioridad:** primero `~`, después `&` y `|`, que tienen la misma prioridad y se evalúan de izquierda a derecha. Por eso `~p | q` (negás solo p) es distinto de `~(p | q)` (negás todo). **Poné siempre paréntesis** y no dependas de la prioridad.
- Una coma en el enunciado agrupa: "hay flor en la esquina y hay papel en la bolsa, o hay papel en la esquina" es `(p & q) | r`.

Para negar una condición compuesta se invierte el conectivo (leyes de De Morgan):

- `~(p & q)` es lo mismo que `~p | ~q`
- `~(p | q)` es lo mismo que `~p & ~q`

Es lo que necesitás para escribir un `mientras`: "caminar **hasta** encontrar una esquina con flor y papel" se escribe "mientras **no** (flor y papel)", o sea `mientras ~(HayFlorEnLaEsquina) | ~(HayPapelEnLaEsquina)`. Y "esquina vacía" es `~(HayFlorEnLaEsquina) & ~(HayPapelEnLaEsquina)`.

## Variables y tipos de datos

Un algoritmo tiene dos partes: el **control** (el orden de las instrucciones) y los **datos** (la información que procesa). Una **variable** guarda un dato que puede cambiar durante la ejecución, y se identifica con un nombre (identificador).

- Se declaran **dentro del robot**, en `variables`, entre `robot robot1` y `comenzar`. En el programa principal solo se declara el robot.
- Se asigna con `:=` (dos puntos igual): `flores := 0`. Primero se calcula lo de la derecha y después se guarda en la de la izquierda, por eso `flores := flores + 1` suma uno.
- Antes de usar una variable para acumular o contar hay que **inicializarla**: darle un valor inicial (casi siempre 0) **antes** de la estructura que la modifica.

| Tipo | Valores | Operaciones | Comparaciones |
|---|---|---|---|
| `numero` | enteros, positivos y negativos | `+` `-` `*` `/` (la división es **entera**: `25 / 3` da 8) | `=` `<` `>` `<=` `>=` `<>` (distinto) |
| `boolean` | `V` o `F` | se combinan con `&` `\|` `~` | |

Una variable `boolean` guarda el resultado de una condición para usarlo después, aunque el robot ya se haya movido: `habiaFlor := HayFlorEnLaEsquina`.

> Antes de declarar una variable, fijate si el robot ya tiene el dato. Para saber cuántas cuadras caminó por una avenida desde la calle 1 no hace falta un contador: alcanza con `PosCa - 1`.

Cuidado con los nombres de los enunciados: **"al menos 5"** es `>= 5`, **"más de 5"** es `> 5`, **"a lo sumo 5"** es `<= 5`, **"exactamente 5"** es `= 5`, **"menos de 5"** es `< 5`.

## Los patrones que aparecen en todos los exámenes

Casi todo ejercicio del curso es una combinación de estas piezas. Si las sabés de memoria, el examen es armarlas.

### Recorrer una avenida o una calle entera

Una avenida tiene 100 esquinas pero **99 cuadras**. Por eso se procesa y se mueve 99 veces, y **la última esquina se procesa aparte**. Olvidar la esquina 100 es el error más común del curso.

```rinfo
programa RecorrerAvenida
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  variables
    papeles: numero
  comenzar
    papeles := 0
    repetir 99
      mientras HayPapelEnLaEsquina
        tomarPapel
        papeles := papeles + 1
      mover
    {la esquina (1,100) se procesa aparte}
    mientras HayPapelEnLaEsquina
      tomarPapel
      papeles := papeles + 1
    Informar(papeles)
  fin
variables
  R-info: robot1
comenzar
  AsignarArea(R-info,ciudad)
  Iniciar(R-info,1,1)
fin
```

Para recorrer otra avenida, primero `Pos(av,1)`. Para una calle, `derecha` y `Pos(1,ca)`. Para un tramo, como de la calle 12 a la 14, son 2 cuadras: `repetir 2` con la última esquina aparte, o procesar las 3 esquinas a mano.

### Vaciar una esquina

```rinfo
mientras HayFlorEnLaEsquina
  tomarFlor
mientras HayPapelEnLaEsquina
  tomarPapel
```

Es `mientras` y no `si`, porque puede haber varias. Para vaciar la bolsa es igual, con `HayFlorEnLaBolsa` y `depositarFlor`.

### Contar sin modificar la esquina

Cuando el enunciado dice "sin modificar" o "no se debe alterar el contenido", tomás contando y después devolvés exactamente lo que tomaste:

```rinfo
cant := 0
mientras HayFlorEnLaEsquina
  tomarFlor
  cant := cant + 1
repetir cant
  depositarFlor
```

Funciona aunque la esquina esté vacía: `cant` queda en 0 y el `repetir` no hace nada. No uses `mientras HayFlorEnLaBolsa depositarFlor` para devolver: dejarías también las flores que el robot ya traía.

### Buscar algo que seguro existe

```rinfo
mientras ~(HayFlorEnLaEsquina)
  mover
```

Solo es válido si el enunciado lo garantiza. Si no, el robot se sale de la ciudad y el programa se corta con error.

### Buscar algo que puede no existir

Se agrega la condición del borde. Cuando el `mientras` termina, hay que averiguar **por qué** terminó: puede haber encontrado lo que buscaba, o haber llegado a la calle 100 (y la esquina 100 también puede ser la buscada).

```rinfo
mientras ~(HayFlorEnLaEsquina) & (PosCa < 100)
  mover
si HayFlorEnLaEsquina
  Informar(PosCa)
sino
  Informar(0)
```

### Juntar hasta llegar a una cantidad

"Caminar hasta juntar 20 flores, puede haber varias por esquina": hay que cortar en cuanto llegás a 20, aunque la esquina tenga más, y no moverte de más.

```rinfo
flores := 0
mientras flores < 20
  mientras HayFlorEnLaEsquina & (flores < 20)
    tomarFlor
    flores := flores + 1
  si flores < 20
    mover
```

Si las 20 pueden no existir, agregá `& (PosCa < 100)` (o `PosAv`, según el recorrido) al `mientras` de afuera y al `si`, y sacá la conclusión al final con un `si`.

### Contar esquinas que cumplen algo

Un contador que se inicializa una vez y se incrementa adentro de un `si`. Por ejemplo, esquinas que tienen **solo** papeles (papel y ninguna flor):

```rinfo
si HayPapelEnLaEsquina & ~(HayFlorEnLaEsquina)
  esquinas := esquinas + 1
```

Si pide "esquinas con exactamente 6 papeles", primero contás los papeles de esa esquina en otra variable (puesta en 0 **en cada esquina**) y después comparás `si papeles = 6`.

### Un dato por avenida (o por calle)

Si se informa algo **por cada** avenida, la variable se pone en 0 **al principio de cada avenida** y se informa **al final de cada avenida**, adentro del `repetir` que las recorre. Si es un total de todo el recorrido, se pone en 0 una vez antes de todo y se informa una vez al final.

### Recorrer toda la ciudad, avenida por avenida

```rinfo
repetir 99
  {procesar la avenida actual}
  Pos(PosAv + 1, 1)
{procesar la avenida 100}
```

Por calles es igual, mirando al este y con `Pos(1, PosCa + 1)`. Como `Pos` no cambia la orientación, el robot sigue mirando hacia donde estaba.

### Avenidas o calles pares e impares

Saltando de a dos: arrancás en la 1 (impares) o en la 2 (pares) y avanzás con `Pos(PosAv + 2, 1)`. Hay 50 de cada una, así que son 49 saltos.

### El perímetro de la ciudad

Cuatro lados de 99 cuadras, girando al final de cada uno:

```rinfo
repetir 4
  repetir 99
    mover
  derecha
```

Si hay que procesar las esquinas, se hace antes de cada `mover`. Así se procesa cada esquina una vez, incluidos los cuatro vértices.

### Cuadrados y rectángulos

Un cuadrado de lado `L` en sentido horario es `repetir 4` (`repetir L` `mover`, después `derecha`). El robot termina en la misma esquina y mirando hacia el mismo lado que al empezar. Un rectángulo alterna alto y ancho: `repetir 2` (`repetir alto` `mover`, `derecha`, `repetir ancho` `mover`, `derecha`).

### Comparar dos cantidades

```rinfo
si flores > papeles
  Informar(flores)
sino
  Informar(papeles)
```

Pensá siempre qué pasa si son **iguales**: acá se informaría `papeles`. Si el enunciado distingue el empate, hace falta otro `si`.

## Modularización: procesos

Un problema grande se divide en **subproblemas** más simples ("divide y vencerás", diseño **Top-Down**). Cada subproblema se resuelve en un **módulo** (en R-info, un **proceso**) que hace una sola tarea bien definida. El programa principal (en el curso, el código del robot) coordina y llama a los procesos.

Las cuatro ventajas que te pueden preguntar:

- **Independencia:** cada módulo se escribe y se prueba por separado. Quien lo usa no necesita saber cómo está hecho.
- **Modificación localizada:** cambiar cómo funciona un módulo por dentro no afecta al resto.
- **Reusabilidad:** el mismo módulo sirve en muchos programas (por ejemplo `Izquierda` o `JuntarFlores`).
- **Mantenimiento:** cada tarea está en un solo lugar, es fácil encontrar qué cambiar.

La modularización no es obligatoria para que un programa funcione, pero **en los exámenes se exige**. Si el enunciado dice "se debe usar modularización (como mínimo un módulo para…)", sin esos módulos el ejercicio no está bien aunque el robot haga lo correcto.

```rinfo
programa ConProcesos
procesos
  proceso JuntarFlores
  comenzar
    mientras HayFlorEnLaEsquina
      tomarFlor
  fin
  proceso Izquierda
  comenzar
    repetir 3
      derecha
  fin
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  comenzar
    JuntarFlores
    mover
    Izquierda
    JuntarFlores
  fin
variables
  R-info: robot1
comenzar
  AsignarArea(R-info,ciudad)
  Iniciar(R-info,1,1)
fin
```

- Los procesos se declaran en la sección `procesos`, **antes** de `areas`.
- Un proceso que llama a otro tiene que estar declarado **después** de él.
- Un proceso puede tener sus propias variables (`variables` entre el encabezado y `comenzar`). Esas **variables locales** solo existen adentro del proceso: ni el robot ni otros procesos las ven. Y el proceso tampoco ve las variables del robot: lo que necesite compartir tiene que entrar por parámetro.
- Cuando se invoca un proceso, el que llama se suspende; al terminar el proceso, la ejecución sigue en la línea siguiente a la invocación.
- Dejá claro en qué esquina y mirando hacia dónde arranca y termina cada proceso. Un cuadrado que vuelve a la esquina y orientación del principio es mucho más fácil de reusar.

## Parámetros de entrada (E) y de entrada/salida (ES)

Un **parámetro** es información que se intercambia entre módulos. Sin parámetros, un proceso hace siempre lo mismo; con ellos, el mismo proceso hace cuadrados de cualquier lado o devuelve lo que contó.

```rinfo
proceso Cuadrado(E lado: numero; ES vertices: numero)
```

- Cada parámetro lleva **clase** (`E` o `ES`), **nombre** y **tipo** (`numero` o `boolean`). Se separan con **punto y coma**.
- **Parámetros formales:** los del encabezado del proceso (`lado`, `vertices`). **Parámetros actuales:** los de la invocación (`Cuadrado(5, total)`). Se corresponden **por posición**, no por nombre: podés cambiarle el nombre a un formal sin tocar la invocación.

| | `E` (entrada) | `ES` (entrada/salida) |
|---|---|---|
| Para qué | el proceso **recibe** un dato | el proceso recibe un dato, lo **modifica** y lo **devuelve** |
| Qué se le puede pasar | un número, una variable o una cuenta (`lado + 1`) | **solo una variable** |
| ¿Se puede asignar adentro? | **no**: el apunte lo marca como inválido y en el examen se corrige como error, aunque el ambiente lo deje correr | sí, y el cambio queda en la variable de quien llamó |
| Uso típico | tamaño de una figura, número de avenida, cuántas flores dejar | contadores y acumuladores, resultados que el proceso calcula |

> **Un parámetro E no se modifica nunca.** Si el proceso necesita cambiar ese valor (por ejemplo, dejar una flor menos en cada esquina), copialo a una variable local y modificá la copia:

```rinfo
proceso UnaMenos(E floresIniciales: numero)
variables
  cuantas: numero
comenzar
  cuantas := floresIniciales
  repetir 10
    repetir cuantas
      depositarFlor
    mover
    cuantas := cuantas - 1
fin
```

- El ES sirve para **acumular**: el robot pone `total := 0` una vez y llama muchas veces `SumarEsquina(total)`. Cada llamada suma sobre lo que ya había.
- También sirve solo como **salida**: el proceso hace `cant := 0` al principio y devuelve lo que contó. En ese caso no importa qué valor traía.
- Elegir bien: si el proceso solo **usa** el dato, E. Si lo **cambia** o lo **produce** para que lo use quien llama, ES. Un ES innecesario resta independencia al módulo.

## Un examen resuelto de punta a punta

Examen 2013: *"Recorrer la avenida 8 juntando todas las flores y todos los papeles hasta encontrar una esquina vacía. Luego recorrer un rectángulo que comience en (1,1), con alto igual a la cantidad de flores juntadas y ancho igual a la cantidad de papeles. Como mínimo debe haber un módulo para la avenida 8 y otro para el rectángulo. La esquina vacía seguro existe. El total de flores y de papeles es menor o igual a 99."*

Antes de escribir una línea, sacá del enunciado:

- **Recorrido:** avenida 8 hacia el norte, con un `mientras` (no se sabe cuántas cuadras).
- **Condición de corte:** esquina vacía, o sea seguir **mientras** haya flor **o** papel. Seguro existe: no hace falta controlar el borde.
- **Datos:** dos contadores, flores y papeles. El proceso de la avenida los produce, así que son **ES**.
- **Rectángulo:** recibe alto y ancho y solo los usa, así que son **E**. Los "≤ 99" garantizan que no se sale de la ciudad.

```rinfo
programa Examen2013
procesos
  proceso Avenida8(ES flores: numero; ES papeles: numero)
  comenzar
    flores := 0
    papeles := 0
    Pos(8,1)
    mientras HayFlorEnLaEsquina | HayPapelEnLaEsquina
      mientras HayFlorEnLaEsquina
        tomarFlor
        flores := flores + 1
      mientras HayPapelEnLaEsquina
        tomarPapel
        papeles := papeles + 1
      mover
  fin
  proceso Rectangulo(E alto: numero; E ancho: numero)
  comenzar
    repetir 2
      repetir alto
        mover
      derecha
      repetir ancho
        mover
      derecha
  fin
areas
  ciudad: AreaC(1,1,100,100)
robots
  robot robot1
  variables
    f: numero
    p: numero
  comenzar
    Avenida8(f, p)
    Pos(1,1)
    Rectangulo(f, p)
  fin
variables
  R-info: robot1
comenzar
  AsignarArea(R-info,ciudad)
  Iniciar(R-info,1,1)
fin
```

Por qué está bien, que es lo mismo que mira quien corrige:

- `Avenida8` arranca sus contadores en 0 y después del `Pos` no gira: el robot ya mira al norte.
- En cada esquina vacía primero toma todo y **después** mueve. Cuando llega a la esquina vacía, el `mientras` de afuera da falso y no se mueve más.
- Después de `Avenida8` el robot sigue mirando al norte y `Pos(1,1)` no cambia eso, así que el rectángulo arranca subiendo: alto primero, como pide el enunciado.
- Si no juntó nada, `repetir 0` no mueve al robot: no hay error.

## Cómo encarar cualquier ejercicio

1. **Leé el enunciado entero dos veces** y marcá las palabras que cambian el código: "seguro existe" / "puede no existir", "sin modificar", "al menos" / "exactamente" / "a lo sumo", "por cada" / "en total", "modularizar".
2. **Dibujá el recorrido** en la cuadrícula: dónde arranca, hacia dónde mira, dónde termina, cuántas cuadras hace.
3. **Decidí la estructura:** ¿la cantidad de pasos se conoce? `repetir`. ¿Depende de lo que encuentre? `mientras`.
4. **Listá los datos** que hay que informar y decidí dónde se inicializa y dónde se informa cada uno (una vez en total, o una vez por avenida).
5. **Separá en módulos:** uno por tarea (procesar una esquina, recorrer una avenida, hacer una figura). Para cada parámetro decidí E o ES.
6. **Escribí primero el programa en comentarios** (`{ir a la avenida 8}`, `{juntar todo}`) y después traducí cada comentario.
7. **Hacé el seguimiento a mano** con los casos de la lista para revisar antes de entregar.

## Los errores que más puntos hacen perder

- **Olvidar la última esquina** de un recorrido de `repetir 99`.
- **Tomar o depositar sin preguntar** (`tomarFlor` sin `HayFlorEnLaEsquina`, `depositarFlor` sin `HayFlorEnLaBolsa`) cuando el enunciado no lo garantiza.
- **Salirse de la ciudad**: `mover` en la calle 100 mirando al norte, o un `mientras` sin control de borde cuando la cosa puede no existir.
- **Usar `si` donde va `mientras`** para juntar todo lo de una esquina: `si` toma uno solo.
- **No inicializar** un contador, o inicializarlo **en el lugar equivocado**: adentro del ciclo si es un total (se borra en cada vuelta), afuera si es por avenida (no se reinicia).
- **Asignar a un parámetro E**, o pasar un número a un parámetro ES.
- **Creer que `Pos` cambia la orientación**: no la cambia.
- **Asignar `PosAv` o `PosCa`**: se leen, no se escriben.
- **Mayúsculas mal escritas** (`Mover`, `tomarflor`, `Hayflorenlaesquina`): no compila.
- **Indentación mal puesta**: una línea con un nivel de más o de menos cambia qué se repite.
- **Modificar las esquinas** cuando el enunciado pide no hacerlo, o devolver de más con `mientras HayFlorEnLaBolsa`.
- **Confundir avenida con calle** o invertir las coordenadas de `Pos(av, ca)`.
- **Leer mal las cantidades**: "al menos" (`>=`) no es "más de" (`>`).
- **No informar** lo que se pide, o informarlo una sola vez cuando se pedía uno por avenida.
- **Negar mal una condición compuesta**: lo contrario de "flor y papel" es "no flor **o** no papel".
- **No modularizar** cuando el enunciado lo exige, o hacer un único proceso que lo hace todo.

## Lista para revisar antes de entregar

Pasá tu programa por estos casos, siguiendo el código línea por línea:

- [ ] La esquina donde arranca el recorrido, ¿se procesa?
- [ ] La última esquina (calle o avenida 100, o el final del tramo), ¿se procesa?
- [ ] Con una esquina **vacía**, ¿hay algún `tomar` que falle?
- [ ] Con la **bolsa vacía**, ¿hay algún `depositar` que falle?
- [ ] Si lo que se busca **no aparece**, ¿el robot se sale de la ciudad?
- [ ] Si un contador queda en **0**, ¿el programa sigue funcionando?
- [ ] ¿Cada variable está inicializada antes de usarse, en el lugar correcto?
- [ ] ¿Cada `Informar` informa lo que pide el enunciado, en el momento que lo pide?
- [ ] ¿Están los módulos que pide el enunciado, con E o ES bien elegidos?
- [ ] ¿Ningún proceso asigna a un parámetro E?
- [ ] ¿Las mayúsculas, la indentación y los nombres de las primitivas están bien?
- [ ] ¿Hacia dónde mira el robot al empezar cada tramo?

## Resumen

- Un algoritmo es una secuencia de pasos elementales, sin ambigüedad, que termina. Tiene precondición y postcondición.
- Cuatro estructuras de control: secuencia, selección (`si`), repetición (`repetir N`, cantidad conocida) e iteración (`mientras`, se evalúa antes de cada vuelta). La indentación define qué pertenece a cada una.
- Esquina = (avenida, calle). El robot arranca en (1,1) mirando al norte y solo gira a la derecha. `Pos` no cambia la orientación.
- Antes de tomar, preguntá si hay en la esquina; antes de depositar, si hay en la bolsa; antes de mover, si no estás en el borde.
- `&` pide las dos, `|` pide al menos una, `~` niega. Usá paréntesis y negá con De Morgan.
- Variables `numero` y `boolean`, declaradas en el robot, asignadas con `:=` e inicializadas antes del ciclo que las usa.
- Una avenida son 99 cuadras: `repetir 99` y la última esquina aparte.
- Procesos para cada tarea. Parámetro E: solo se lee. Parámetro ES: se lee, se modifica y vuelve; el actual tiene que ser una variable.
