# Conocimiento — EPA en Markdown

Esta carpeta es la capa de conocimiento educativo del repositorio: contiene los 10 documentos del curso convertidos a Markdown estructurado, organizados por unidad, trazables hasta su PDF original y reutilizables por personas y por sistemas de IA.

- **Índice completo:** [INDICE_GENERAL.md](INDICE_GENERAL.md) — catálogo por unidad, tema, nivel, lenguaje, tipo y prerrequisitos.
- **Glosario:** [GLOSARIO.md](GLOSARIO.md) — términos centrales del curso con enlace a su explicación.
- **Instrucciones de organización:** `../prompt-organizacion/` (requiere_revision — la carpeta no existe en este repositorio ni en su historial de Git).

## Estructura de cada unidad

Cada `unidad-NN-tema/` contiene, según lo que exista para ese capítulo:

```text
unidad-NN-tema/
├── README.md            Mapa de la unidad: qué enseña, prerrequisitos, cómo seguir
├── <capitulo>.md         Teoría convertida del PDF, con ejercitación incluida
├── fuentes/              PDF original de ese capítulo
├── recursos/             Imágenes y figuras propias del capítulo
└── codigo/
    ├── ejemplos/         Programas breves para estudiar un concepto puntual
    └── soluciones/       Resoluciones de los ejercicios del capítulo
```

No todas las unidades usan todas las piezas: las unidades 0 y 1 no tienen código porque son previas a la presentación de R-info.

## Unidades

| # | Unidad | Carpeta | Contenido principal |
|---:|---|---|---|
| 0 | Presentación e introducción al curso | [unidad-00-introduccion](unidad-00-introduccion/) | Índice general, bienvenida, cómo estudiar |
| 1 | Resolución de problemas | [unidad-01-resolucion-de-problemas](unidad-01-resolucion-de-problemas/) | Algoritmos y estructuras de control |
| 2 | Algoritmos, lógica y R-info | [unidad-02-algoritmos-y-logica](unidad-02-algoritmos-y-logica/) | R-info, lógica y tablas de verdad |
| 3 | Datos y variables | [unidad-03-datos](unidad-03-datos/) | Variables, tipos y datos |
| 4 | Repaso integrador | [unidad-04-repaso](unidad-04-repaso/) | Problemas integradores |
| 5 | Programación estructurada | [unidad-05-programacion-estructurada](unidad-05-programacion-estructurada/) | Top-Down y modularización |
| 6 | Parámetros de entrada | [unidad-06-parametros-de-entrada](unidad-06-parametros-de-entrada/) | Parámetros de entrada |
| 7 | Parámetros de entrada/salida | [unidad-07-parametros-de-entrada-salida](unidad-07-parametros-de-entrada-salida/) | Parámetros de entrada/salida |
| 8 | Práctica adicional y exámenes | [unidad-08-practica-adicional](unidad-08-practica-adicional/) | Práctica integradora y exámenes 2013 |

## Cómo interpretar los metadatos de cada archivo

Cada capítulo comienza con un front matter YAML (`id`, `titulo`, `tipo`, `unidad`, `tema`, `subtemas`, `nivel`, `lenguajes`, `estado`, `origen`, `fuentes`, `prerrequisitos`, `relacionados`, `codigo_relacionado`). Estos campos permiten:

- Ubicar de qué PDF y con qué alcance de páginas proviene el contenido (`fuentes`).
- Saber qué unidades hay que leer antes (`prerrequisitos`) y qué sigue (`relacionados`).
- Encontrar el código ejecutable asociado sin tener que buscarlo manualmente (`codigo_relacionado`).
- Distinguir contenido `convertido` (proviene del PDF original) de contenido `generado` o `corregido`; en esta carpeta **todo el contenido es `origen: "convertido"`**, no hay texto generado por IA.

## Cómo usar esta carpeta como contexto para una IA

Para pedir un proyecto integrador, una clase o una guía de estudio basada en este material, referenciá directamente los capítulos y su front matter (por ejemplo, "usando los conceptos de `CON-EPA-U05-PROG-ESTRUCTURADA` y `CON-EPA-U06-PARAMETROS-ENTRADA`, generá..."). El `id` de cada archivo es estable y puede citarse en pedidos futuros.

## Recorrido recomendado

Introducción → Resolución de problemas → Algoritmos y R-info → Datos y variables → Repaso → Programación estructurada → Parámetros de entrada → Parámetros de entrada/salida → Ejercicios adicionales.

## Cómo usar los enlaces al código

Al final de las unidades 2 a 7 se incluye una tabla que relaciona cada ejercicio con los archivos de solución existentes. En las unidades 2 y 3 están directamente en `codigo/` (archivos `.ri`); en las unidades 4 a 7 siguen en `codigo/soluciones/` dentro de cada unidad, con archivos sin extensión que también contienen código R-info en texto plano y pueden abrirse directamente desde VS Code.

Los nombres heredados ambiguos de la unidad 2 no se vincularon a ejercicios concretos sin evidencia suficiente; quedaron como `codigo-01.ri`…`codigo-10.ri` en [unidad-02-algoritmos-y-logica/codigo](unidad-02-algoritmos-y-logica/codigo/) para revisión manual.

## Ejercicios atomizados por archivo (convención de `AYP1-FABOSISTEMAS`)

Las 7 unidades de EPA con R-info (unidad-02 a unidad-08) adoptaron la misma atomización que ya usa `AYP1-FABOSISTEMAS`: además del capítulo completo, cada ejercicio con código identificado y verificado contra su propio enunciado tiene su propio archivo en `ejercicios/` (enunciado + front matter) y `soluciones/` (análisis, estrategia, código, casos límite, errores frecuentes), enlazados entre sí y con `codigo_relacionado` apuntando al `.ri` (o al archivo sin extensión correspondiente, según la unidad). La cobertura varía por unidad — desde los 8 de 8 ejercicios de la ejercitación en unidad-06 hasta 2 de 6 en unidad-07 — porque bastante código histórico resultó implementar un problema distinto al de su propio enunciado; ese código queda señalado como pendiente en el `README.md` de cada unidad en vez de reescribirse. Ver [INDICE_GENERAL.md](INDICE_GENERAL.md#notas-de-procedencia) para el resumen con el link a cada unidad. Es la estructura que lee [Academia-Fabo](https://github.com/Fabian-Martinez-Rincon/Academia-Fabo) para mostrar cada ejercicio con un runner de R-info (intérprete propio, no el `.jar` original) en el navegador.

> Algunas soluciones son apuntes históricos y pueden contener variantes o intentos intermedios. Se recomienda compilarlas en R-info y compararlas con las precondiciones y postcondiciones del enunciado.
