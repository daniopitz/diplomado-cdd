# Evaluación 2: Primer análisis exploratorio de datos

Diplomado en Ciencia de Datos Aplicada, Módulo 1: Introducción y fundamentos
estadísticos. Ponderación: 40% del módulo. Resultado de aprendizaje RA1.1.

El primer análisis exploratorio aplica a los datos del proyecto lo trabajado en
las clases 2 a 4: describir, limpiar, relacionar y graficar, con el norte
puesto en los modelos que vienen. Se evalúa con la
[rúbrica publicada](rubricas/rubrica_eda_capstone.md), que conviene leer antes
de empezar.

## Condiciones de entrega

- Equipos de dos personas; un envío por equipo, con los nombres de sus
  integrantes.
- Un notebook de Jupyter (.ipynb) ejecutado de principio a fin, con NumPy,
  Pandas y Matplotlib, por el aula virtual. Si los datos no se pueden adjuntar
  (por tamaño o confidencialidad), el notebook debe indicar cómo obtenerlos o
  incluir una muestra que permita ejecutarlo.
- NumPy, Pandas y Matplotlib son la base que pide el programa, no un límite:
  se pueden usar además otras bibliotecas de ciencia de datos (seaborn, SciPy
  y similares), sin penalización.
- Fecha de entrega: lunes 15 de septiembre de 2026.

## Qué debe contener el notebook

El notebook se organiza en cinco secciones, una por criterio de la rúbrica.
Antes de cada análisis, declare su objetivo en una línea: qué se quiere
relacionar o revisar, y por qué.

1. **Los datos y su calidad.** La carga desde su fuente (declarada), el tamaño
   de las tablas y los tipos de variables. La revisión de calidad de la
   clase 2: valores faltantes (incluidos los disfrazados, como códigos 999 o
   valores −1), duplicados y valores imposibles según el dominio; si hay
   merges, verificados con conteos antes y después. Cada decisión de limpieza
   se documenta en una línea.
2. **Estadística descriptiva.** Tendencia central, dispersión y forma de las
   variables relevantes, con su interpretación en el contexto del problema.
   Si sus datos traen factores de expansión o pesos de muestreo, úselos.
3. **Análisis bivariado.** Las relaciones que apuntan a su pregunta:
   correlaciones (Pearson, y Spearman cuando hay atípicos o curvas), la matriz
   de correlación si hay varias cuantitativas, y grupos o tablas de
   contingencia si hay categóricas. Interprete lo que los datos muestran, no
   más que eso.
4. **Visualización.** Al menos tres gráficos de tipos distintos, elegidos
   según la variable y la pregunta (histograma, boxplot, dispersión, barras,
   línea de tendencia u otros). Todos rotulados (ejes con nombre y unidad) y
   con el hallazgo en el título; el overplotting y las colas largas se tratan
   cuando aparecen (transparencia, hexbin, escala logarítmica).
5. **Hallazgos y siguientes pasos.** De 3 a 5 hallazgos escritos en frases
   completas, y qué modelo imaginan ajustar en el avance del proyecto.

## Uso de inteligencia artificial

Se aplica la regla del módulo: el uso de IA generativa está permitido con
declaración (qué herramienta se usó y para qué). Debe entender y poder
explicar cualquier parte de lo que entregue.
