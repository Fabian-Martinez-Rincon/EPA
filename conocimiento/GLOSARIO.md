# Glosario — EPA (Expresión de Problemas y Algoritmos)

Términos centrales del curso, con una definición breve y el capítulo donde se explican en detalle. Enlaza al archivo completo del capítulo; buscá el subtítulo indicado entre paréntesis para ubicar la explicación exacta.

## Algoritmos y resolución de problemas

- **Algoritmo**: secuencia finita y ordenada de pasos que resuelve un problema. Ver [Unidad 1](<unidad-01-resolucion-de-problemas/capitulo-1-resolucion-de-problemas.md>) (sección "1.3 Algoritmo").
- **Precondición**: condición que debe cumplirse antes de ejecutar un algoritmo para garantizar su correcto funcionamiento. Ver [Unidad 1](<unidad-01-resolucion-de-problemas/capitulo-1-resolucion-de-problemas.md>) (sección "1.4 Pre y Postcondiciones de un algoritmo").
- **Postcondición**: condición que se cumple al finalizar la ejecución de un algoritmo, si las precondiciones eran válidas. Ver [Unidad 1](<unidad-01-resolucion-de-problemas/capitulo-1-resolucion-de-problemas.md>).
- **Secuencia**: estructura de control donde las acciones se ejecutan una tras otra, en el orden en que aparecen. Ver [Unidad 1](<unidad-01-resolucion-de-problemas/capitulo-1-resolucion-de-problemas.md>) (sección "1.5.1").
- **Selección**: estructura de control que ejecuta una u otra acción según se cumpla o no una condición (`si` / `sino`). Ver [Unidad 1](<unidad-01-resolucion-de-problemas/capitulo-1-resolucion-de-problemas.md>) (sección "1.5.2") y [Unidad 2](<unidad-02-algoritmos-y-logica/capitulo-2-algoritmos-y-logica.md>) (sección "2.3.2").
- **Repetición**: estructura de control que ejecuta un bloque una cantidad fija de veces (`repetir N`). Ver [Unidad 1](<unidad-01-resolucion-de-problemas/capitulo-1-resolucion-de-problemas.md>) (sección "1.5.3") y [Unidad 2](<unidad-02-algoritmos-y-logica/capitulo-2-algoritmos-y-logica.md>) (sección "2.3.3").
- **Iteración**: estructura de control que ejecuta un bloque mientras se cumpla una condición (`mientras`), sin una cantidad fija de repeticiones. Ver [Unidad 1](<unidad-01-resolucion-de-problemas/capitulo-1-resolucion-de-problemas.md>) (sección "1.5.4") y [Unidad 2](<unidad-02-algoritmos-y-logica/capitulo-2-algoritmos-y-logica.md>) (sección "2.3.4").

## Lenguaje del robot R-info

- **R-info**: lenguaje y entorno de programación de un robot que se mueve en una ciudad cuadriculada, usado en todo el curso a partir de la Unidad 2. Herramienta disponible en [herramientas/r-info-2.9.jar](../herramientas/r-info-2.9.jar). Ver [Unidad 2](<unidad-02-algoritmos-y-logica/capitulo-2-algoritmos-y-logica.md>).
- **Área (`AreaC`)**: definición del tamaño de la ciudad donde se mueve el robot (esquinas, avenidas y calles). Ver [Unidad 2](<unidad-02-algoritmos-y-logica/capitulo-2-algoritmos-y-logica.md>) (sección "2.2.2 Estructura general de un programa").
- **Esquina**: intersección entre una avenida y una calle; puede contener flores y/o papeles. Ver [Unidad 2](<unidad-02-algoritmos-y-logica/capitulo-2-algoritmos-y-logica.md>).
- **Avenida / Calle**: ejes de la grilla de la ciudad; el robot se desplaza y orienta sobre ellos. Ver [Unidad 2](<unidad-02-algoritmos-y-logica/capitulo-2-algoritmos-y-logica.md>).
- **Proceso**: unidad modular de código en R-info, equivalente a un procedimiento o función con nombre propio, reutilizable desde el programa principal u otros procesos. Ver [Unidad 5](<unidad-05-programacion-estructurada/capitulo-5-programacion-estructurada.md>) (sección "5.2 Programación modular").

## Lógica proposicional

- **Proposición atómica**: afirmación simple que puede evaluarse como verdadera o falsa, sin conectores lógicos. Ver [Unidad 2](<unidad-02-algoritmos-y-logica/capitulo-2-algoritmos-y-logica.md>) (sección "2.4.1").
- **Proposición molecular**: combinación de proposiciones atómicas mediante conectivos lógicos (`&`, `|`, `~`). Ver [Unidad 2](<unidad-02-algoritmos-y-logica/capitulo-2-algoritmos-y-logica.md>) (sección "2.4.1").
- **Tabla de verdad**: representación de todos los valores posibles de una proposición molecular según sus componentes. Ver [Unidad 2](<unidad-02-algoritmos-y-logica/capitulo-2-algoritmos-y-logica.md>) (sección "2.4.3").
- **Conjunción / Disyunción / Negación**: operadores lógicos `&`, `|` y `~` respectivamente. Ver [Unidad 2](<unidad-02-algoritmos-y-logica/capitulo-2-algoritmos-y-logica.md>) (secciones "2.4.3.1" a "2.4.3.3").

## Datos y variables

- **Variable**: espacio con nombre propio que almacena un dato de un tipo determinado durante la ejecución del programa. Ver [Unidad 3](<unidad-03-datos/capitulo-3-datos.md>) (sección "3.3 Variables").
- **Tipo de dato numérico**: variable que almacena valores numéricos enteros. Ver [Unidad 3](<unidad-03-datos/capitulo-3-datos.md>) (sección "3.4.1").
- **Tipo de dato lógico (`boolean`)**: variable que almacena verdadero o falso. Ver [Unidad 3](<unidad-03-datos/capitulo-3-datos.md>) (sección "3.4.2").

## Programación estructurada y modularización

- **Descomposición Top-Down**: técnica de diseño que divide un problema grande en subproblemas más simples y manejables. Ver [Unidad 5](<unidad-05-programacion-estructurada/capitulo-5-programacion-estructurada.md>) (sección "5.1").
- **Modularización**: organización del código en procesos independientes y reutilizables. Ver [Unidad 5](<unidad-05-programacion-estructurada/capitulo-5-programacion-estructurada.md>) (sección "5.2") y ejemplos en [codigo/ejemplos/modularizacion](unidad-05-programacion-estructurada/codigo/ejemplos/modularizacion/).
- **Parámetro de entrada (`E`)**: dato que un proceso recibe desde quien lo invoca, sin poder modificarlo para el que llama. Ver [Unidad 6](<unidad-06-parametros-de-entrada/capitulo-6-parametros-de-entrada.md>) y ejemplos en [codigo/ejemplos/parametros-entrada](unidad-06-parametros-de-entrada/codigo/ejemplos/parametros-entrada/).
- **Parámetro de entrada/salida (`ES`)**: dato que un proceso recibe y puede modificar, devolviendo el nuevo valor a quien lo invocó. Ver [Unidad 7](<unidad-07-parametros-de-entrada-salida/capitulo-7-parametros-de-entrada-salida.md>) y ejemplos en [codigo/ejemplos/parametros-entrada-salida](unidad-07-parametros-de-entrada-salida/codigo/ejemplos/parametros-entrada-salida/).

## Ver también

- [Índice general](INDICE_GENERAL.md)
- [Portada de la base de conocimiento](README.md)
