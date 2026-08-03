# EPA - Expresión de Problemas y Algoritmos

Material de estudio, ejercicios y soluciones en R-info para el curso de ingreso de la Facultad de Informática de la UNLP.

## Empezar a estudiar

La forma más simple de recorrer el repositorio es leer cada unidad en `conocimiento/` y, al llegar a la ejercitación, abrir las soluciones enlazadas al final del mismo documento.

| Orden | Tema | Lectura | PDF original | Soluciones |
|---:|---|---|---|---|
| 0 | Introducción al curso | [Unidad 0](<conocimiento/unidad-00-introduccion/capitulo-0-introduccion.md>) | [PDF](<conocimiento/unidad-00-introduccion/fuentes/Capitulo 0-Introduccion.pdf>) | - |
| 1 | Resolución de problemas | [Unidad 1](<conocimiento/unidad-01-resolucion-de-problemas/capitulo-1-resolucion-de-problemas.md>) | [PDF](<conocimiento/unidad-01-resolucion-de-problemas/fuentes/Capitulo 1-Resolucion de problemas.pdf>) | Ejercicios conceptuales |
| 2 | Algoritmos, lógica y R-info | [Unidad 2](<conocimiento/unidad-02-algoritmos-y-logica/capitulo-2-algoritmos-y-logica.md>) | [PDF](<conocimiento/unidad-02-algoritmos-y-logica/fuentes/Capitulo 2-Algoritmos y Logica.pdf>) | [Unidad 2](conocimiento/unidad-02-algoritmos-y-logica/codigo/) |
| 3 | Datos y variables | [Unidad 3](<conocimiento/unidad-03-datos/capitulo-3-datos.md>) | [PDF](<conocimiento/unidad-03-datos/fuentes/Capitulo 3-Datos.pdf>) | [Unidad 3](conocimiento/unidad-03-datos/codigo/) |
| 4 | Repaso integrador | [Unidad 4](<conocimiento/unidad-04-repaso/capitulo-4-repaso.md>) | [PDF](<conocimiento/unidad-04-repaso/fuentes/Capitulo 4-Repaso.pdf>) | [Unidad 4](conocimiento/unidad-04-repaso/codigo/soluciones/capitulo-04/) |
| 5 | Programación estructurada | [Unidad 5](<conocimiento/unidad-05-programacion-estructurada/capitulo-5-programacion-estructurada.md>) | [PDF](<conocimiento/unidad-05-programacion-estructurada/fuentes/Capitulo 5-Programacion Estructurada.pdf>) | [Unidad 5](conocimiento/unidad-05-programacion-estructurada/codigo/soluciones/capitulo-05/) |
| 6 | Parámetros de entrada | [Unidad 6](<conocimiento/unidad-06-parametros-de-entrada/capitulo-6-parametros-de-entrada.md>) | [PDF](<conocimiento/unidad-06-parametros-de-entrada/fuentes/Capitulo 6-Parametros de Entrada.pdf>) | [Unidad 6](conocimiento/unidad-06-parametros-de-entrada/codigo/soluciones/capitulo-06/) |
| 7 | Parámetros de entrada/salida | [Unidad 7](<conocimiento/unidad-07-parametros-de-entrada-salida/capitulo-7-parametros-de-entrada-salida.md>) | [PDF](<conocimiento/unidad-07-parametros-de-entrada-salida/fuentes/Capitulo 7-Parametros de Entrada-Salida.pdf>) | [Unidad 7](conocimiento/unidad-07-parametros-de-entrada-salida/codigo/soluciones/capitulo-07/) |
| 8 | Práctica adicional | [Ejercicios adicionales](<conocimiento/unidad-08-practica-adicional/ejercicios-adicionales.md>) | [PDF](<conocimiento/unidad-08-practica-adicional/fuentes/Ejercicios Adicionales.pdf>) | [Práctica guiada](conocimiento/unidad-08-practica-adicional/practica-guiada.md) |

También podés entrar desde el [índice completo de conocimiento](conocimiento/README.md), que reúne todas las unidades y sus PDF, o desde el [índice general para IA](conocimiento/INDICE_GENERAL.md) y el [glosario de términos](conocimiento/GLOSARIO.md).

## Método de estudio recomendado

1. Leé la unidad en Markdown y observá las figuras originales.
2. Intentá resolver la ejercitación sin consultar el código.
3. Compará tu propuesta con las soluciones enlazadas al final del capítulo.
4. Abrí el archivo en R-info, compilalo y probalo con distintas configuraciones de ciudad.
5. Revisá precondiciones, postcondiciones, casos límite y si el recorrido modifica flores o papeles.

Las soluciones representan alternativas de resolución; no necesariamente son las únicas ni todas tienen el mismo nivel de revisión.

## Organización del repositorio

```text
EPA/
├── prompt-organizacion/          Instrucciones para mantener esta base de conocimiento (requiere_revision: carpeta no encontrada en este repositorio)
├── conocimiento/                 Base de conocimiento educativa (capa principal)
│   ├── README.md, INDICE_GENERAL.md, GLOSARIO.md
│   └── unidad-00-introduccion/ … unidad-08-practica-adicional/
│       ├── <capitulo>.md         Teoría convertida + ejercitación
│       ├── ejercicios/, soluciones/  Unidades 02-08: parte de la ejercitación
│       │                             atomizada uno por archivo (convención de AYP1-FABOSISTEMAS);
│       │                             cobertura parcial y distinta por unidad, ver INDICE_GENERAL.md
│       ├── fuentes/              PDF original de esa unidad
│       ├── recursos/             Imágenes propias de esa unidad
│       └── codigo/
│           ├── ejemplos/         Programas breves por concepto
│           └── soluciones/       Ejercicios resueltos
├── Estudiantes/                  Trabajos de estudiantes (exámenes voluntarios)
├── Recursos/                     Imágenes generales del repositorio (no ligadas a una unidad)
├── herramientas/                 Ejecutable de R-info
└── LICENSE
```

## Ejecutar los programas

Los programas del curso usan el lenguaje del robot R-info. El entorno está disponible en [herramientas/r-info-2.9.jar](herramientas/r-info-2.9.jar).

Requisitos:

- Java instalado.
- Un editor de texto como Visual Studio Code para revisar los archivos.
- R-info para compilar, configurar la ciudad y ejecutar los recorridos.

Los archivos `.ri` y varios archivos históricos sin extensión contienen código de texto plano. Si un archivo no se abre automáticamente, elegí abrirlo como texto.

## Recursos complementarios

- [Base de conocimiento completa](conocimiento/README.md)
- [Resumen de EPA en video](https://www.youtube.com/watch?v=fDYjor2P-YQ)
- [Exámenes voluntarios](Estudiantes/)
- Instrucciones de organización del repositorio: `prompt-organizacion/` (requiere_revision — la carpeta no existe en este repositorio ni en su historial de Git; si el contenido vive en otra ubicación, falta enlazarlo o copiarlo aquí)

## Nota sobre el material histórico

Algunos archivos conservan nombres originales poco descriptivos porque forman parte del historial del repositorio. Están agrupados por unidad, dentro de `codigo/soluciones/` de cada una, para que no interfieran con el recorrido principal. La copia antigua de soluciones del capítulo 6 está separada en [conocimiento/unidad-06-parametros-de-entrada/codigo/archivo-historico/duplicado-capitulo-06](conocimiento/unidad-06-parametros-de-entrada/codigo/archivo-historico/duplicado-capitulo-06/).
