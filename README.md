# Introducción y fundamentos estadísticos

Módulo 1 del [Diplomado en Ciencia de Datos Aplicada](https://informatica.usm.cl/diplomado-ciencia-de-datos-aplicada/),
Departamento de Informática, Universidad Técnica Federico Santa María.
Programa de posgrado (10 créditos SCT en total). Profesora del módulo: Daniela Opitz.

Modalidad 100% online sincrónica. Clases los **martes y jueves de 18:00 a 20:30**,
desde el martes 25 de agosto al martes 22 de septiembre de 2026. El jueves 17 de
septiembre no hay clases por ser preferiado; la clase 8 se dicta el martes 22.

Audiencia: profesionales con grado de licenciatura, con conocimientos de nivel
medio a avanzado en programación en Python y nociones básicas de análisis de
datos. La asignatura se aprueba con una calificación mínima de 60%.

## Contenidos del módulo

- Ciencia de datos: historia y fundamentos conceptuales.
- Ciclo de vida de proyectos de ciencia de datos.
- Ecosistema Python para ciencia de datos: NumPy, Pandas y Matplotlib.
- Tipos de datos y tipos de variables.
- Estadística descriptiva.
- Análisis exploratorio de datos (EDA).
- Fundamentos de probabilidad.
- Nociones básicas de inferencia estadística.
- Regresión lineal, regresión regularizada (Ridge y Lasso) y regresión logística.
- Reducción de dimensionalidad.

## Calendario de clases

Ocho clases de dos horas y media (18:00 a 20:30), en dos bloques de unos 70
minutos con un recreo de 10 minutos a mitad de clase. Las fechas corresponden al
calendario oficial del diplomado y son firmes; los temas de cada clase pueden
ajustarse sobre la marcha según el avance del grupo.

| # | Fecha | Contenidos | Slides | Notebook | Colab |
|---|-------|------------|--------|----------|-------|
| 1 | ma 25-ago | Ciencia de datos: historia y fundamentos conceptuales. Ciclo de vida de proyectos. Tipos de datos y tipos de variables. Ecosistema Python para ciencia de datos: NumPy, Pandas y Matplotlib. Puesta en marcha del entorno con uv y Jupyter | [PDF](presentaciones/clase01_fundamentos_ecosistema.pdf) | [notebook](01_intro_ecosistema.ipynb) | [abrir en Colab](https://colab.research.google.com/github/daniopitz/diplomado-cdd/blob/main/01_intro_ecosistema_colab.ipynb) |
| 2 | ju 27-ago | Estadística descriptiva: medidas de tendencia central, dispersión y forma | | | |
| 3 | ma 01-sep | Análisis exploratorio de datos (EDA): univariado, bivariado, correlación y visualización con Matplotlib | | | |
| 4 | ju 03-sep | Fundamentos de probabilidad: variables aleatorias y distribuciones | | | |
| 5 | ma 08-sep | Nociones de inferencia estadística: estimación, intervalos de confianza y pruebas de hipótesis | | | |
| 6 | ju 10-sep | Regresión lineal simple y múltiple | | | |
| 7 | ma 15-sep | Regresión regularizada (Ridge y Lasso) y regresión logística | | | |
| | ju 17-sep | Sin clases (suspendida por ser preferiado) | | | |
| 8 | ma 22-sep | Reducción de dimensionalidad (PCA) y cierre del módulo | | | |

## Evaluación: proyecto final

El módulo se evalúa con un proyecto final aplicado sobre datos reales, que
recorre el ciclo completo visto en el curso: pregunta, datos, exploración,
análisis y comunicación de resultados. El enunciado, la pauta y la fecha de
entrega se publican durante las primeras clases del módulo.

## Material

La instalación del entorno de trabajo (Python, uv y Jupyter) se explica en la
clase 1, siguiendo la [guía de instalación](guia_instalacion.md); el entorno debe
quedar funcionando antes de la clase 2. El material de cada clase (slides en PDF
y notebook en Python) se enlaza en la tabla del calendario a medida que se
publica.

Cada clase tiene dos notebooks equivalentes: uno para el entorno local del curso
y una versión para Google Colab, que se abre con el enlace "abrir en Colab" de la
tabla y corre sin instalar nada. En ambos, los datos se leen desde una URL.

Algunos conjuntos de datos son compartidos con el curso INF-396 de pregrado,
entre ellos la Encuesta Origen Destino de Santiago 2012 y los registros de
emisiones al aire (RETC 2020).

Como lectura complementaria de acceso abierto se recomienda el
[Python Data Science Handbook](https://jakevdp.github.io/PythonDataScienceHandbook/)
de Jake VanderPlas (versión completa en línea, con notebooks ejecutables en
Colab): sus capítulos de NumPy, Pandas y Matplotlib acompañan las primeras
clases, y el de regresión lineal, la clase 7.
