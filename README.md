# EPA - Expresión de Problemas y Algoritmos

Material de estudio, ejercicios y soluciones en R-info para el curso de ingreso de la Facultad de Informática de la UNLP.

## Empezar a estudiar

La forma más simple de recorrer el repositorio es leer cada capítulo en Markdown y, al llegar a la ejercitación, abrir las soluciones enlazadas al final del mismo documento.

| Orden | Tema | Lectura | PDF original | Soluciones |
|---:|---|---|---|---|
| 0 | Introducción al curso | [Capítulo 0](<material/markdown/Capitulo 0-Introduccion.md>) | [PDF](<material/pdf/Capitulo 0-Introduccion.pdf>) | - |
| 1 | Resolución de problemas | [Capítulo 1](<material/markdown/Capitulo 1-Resolucion de problemas.md>) | [PDF](<material/pdf/Capitulo 1-Resolucion de problemas.pdf>) | Ejercicios conceptuales |
| 2 | Algoritmos, lógica y R-info | [Capítulo 2](<material/markdown/Capitulo 2-Algoritmos y Logica.md>) | [PDF](<material/pdf/Capitulo 2-Algoritmos y Logica.pdf>) | [Capítulo 2](soluciones/por-capitulo/capitulo-02) |
| 3 | Datos y variables | [Capítulo 3](<material/markdown/Capitulo 3-Datos.md>) | [PDF](<material/pdf/Capitulo 3-Datos.pdf>) | [Capítulo 3](soluciones/por-capitulo/capitulo-03) |
| 4 | Repaso integrador | [Capítulo 4](<material/markdown/Capitulo 4-Repaso.md>) | [PDF](<material/pdf/Capitulo 4-Repaso.pdf>) | [Capítulo 4](soluciones/por-capitulo/capitulo-04) |
| 5 | Programación estructurada | [Capítulo 5](<material/markdown/Capitulo 5-Programacion Estructurada.md>) | [PDF](<material/pdf/Capitulo 5-Programacion Estructurada.pdf>) | [Capítulo 5](soluciones/por-capitulo/capitulo-05) |
| 6 | Parámetros de entrada | [Capítulo 6](<material/markdown/Capitulo 6-Parametros de Entrada.md>) | [PDF](<material/pdf/Capitulo 6-Parametros de Entrada.pdf>) | [Capítulo 6](soluciones/por-capitulo/capitulo-06) |
| 7 | Parámetros de entrada/salida | [Capítulo 7](<material/markdown/Capitulo 7-Parametros de Entrada-Salida.md>) | [PDF](<material/pdf/Capitulo 7-Parametros de Entrada-Salida.pdf>) | [Capítulo 7](soluciones/por-capitulo/capitulo-07) |
| 8 | Práctica adicional | [Ejercicios adicionales](<material/markdown/Ejercicios Adicionales.md>) | [PDF](<material/pdf/Ejercicios Adicionales.pdf>) | [Actividad adicional](actividades/adicionales) |

También podés entrar desde el [índice completo del material](material/markdown/README.md), que reúne todos los capítulos y sus PDF.

## Método de estudio recomendado

1. Leé el capítulo en Markdown y observá las figuras originales.
2. Intentá resolver la ejercitación sin consultar el código.
3. Compará tu propuesta con las soluciones enlazadas al final del capítulo.
4. Abrí el archivo en R-info, compilalo y probalo con distintas configuraciones de ciudad.
5. Revisá precondiciones, postcondiciones, casos límite y si el recorrido modifica flores o papeles.

Las soluciones representan alternativas de resolución; no necesariamente son las únicas ni todas tienen el mismo nivel de revisión.

## Organización del repositorio

```text
EPA/
├── material/
│   ├── markdown/                 Libro convertido, imágenes e índice
│   └── pdf/                      Documentos originales
├── soluciones/
│   ├── por-capitulo/             Ejercicios resueltos de los capítulos 2 a 7
│   └── archivo-historico/        Copias antiguas conservadas como referencia
├── ejemplos/
│   ├── modularizacion/
│   ├── parametros-entrada/
│   └── parametros-entrada-salida/
├── actividades/adicionales/      Enunciados, animaciones y soluciones extra
├── entregas/estudiantes/         Trabajos de estudiantes
├── assets/                       Imágenes generales del repositorio
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

- [Ejemplos temáticos](ejemplos/README.md)
- [Índice de soluciones](soluciones/README.md)
- [Actividad adicional](actividades/adicionales/README.md)
- [Resumen de EPA en video](https://www.youtube.com/watch?v=fDYjor2P-YQ)
- [Exámenes voluntarios](entregas/estudiantes)

## Nota sobre el material histórico

Algunos archivos conservan nombres originales poco descriptivos porque forman parte del historial del repositorio. Están agrupados por capítulo para que no interfieran con el recorrido principal. La copia antigua de soluciones del capítulo 6 está separada en `soluciones/archivo-historico/duplicado-capitulo-06`.
