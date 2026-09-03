# Rúbrica: Primer análisis exploratorio de datos

Diplomado en Ciencia de Datos Aplicada, Módulo 1: Introducción y fundamentos
estadísticos. Ponderación: 40% del módulo. Resultado de aprendizaje RA1.1.

## Entrega

- Equipos de dos personas; un envío por equipo, con los nombres de sus
  integrantes.
- Un notebook de Jupyter (.ipynb) ejecutado de principio a fin, con NumPy,
  Pandas y Matplotlib, por el aula virtual.
- Fecha de entrega: lunes 15 de septiembre de 2026.

## Qué se evalúa

Según el programa de la asignatura, esta evaluación mide el desarrollo de
código en el ecosistema Python (NumPy, Pandas y Matplotlib) para explorar los
datos del propio proyecto. El notebook debe cubrir los cinco criterios de la
tabla; el [enunciado](../eda_capstone.md) detalla qué va en cada sección.

| Criterio | Logrado | Parcialmente logrado | No logrado | Puntaje |
|----------|---------|----------------------|------------|---------|
| 1. Los datos y su calidad | Carga desde una fuente declarada, tipos revisados; faltantes (incluidos los disfrazados), duplicados y valores imposibles detectados y resueltos, con cada decisión documentada; merges verificados (17 a 20 pts) | Revisión parcial: detecta problemas pero no documenta decisiones, o pasa por alto faltantes disfrazados y rangos del dominio (9 a 16 pts) | Los datos se usan tal cual, sin revisión de calidad (0 a 8 pts) | 20 |
| 2. Estadística descriptiva | Centro, dispersión y forma de las variables relevantes, interpretados en el contexto del problema; usa los pesos o factores de expansión cuando los datos los traen (17 a 20 pts) | Resúmenes calculados pero poco interpretados, o resúmenes sensibles (media, desviación) donde los robustos correspondían (9 a 16 pts) | Resúmenes ausentes o sin relación con la pregunta del proyecto (0 a 8 pts) | 20 |
| 3. Análisis bivariado | Cada análisis declara su objetivo; correlaciones bien elegidas (Pearson y Spearman) e interpretadas por lo que los datos muestran; matriz, grupos o tablas de contingencia según los tipos de variables, apuntando a la pregunta del proyecto (21 a 25 pts) | Relaciones calculadas pero sin objetivo declarado, o con interpretaciones que van más allá de lo que los datos muestran (11 a 20 pts) | Sin análisis de relaciones, o relaciones ajenas a la pregunta (0 a 10 pts) | 25 |
| 4. Visualización | Gráficos rotulados con nombre y unidad en los ejes y el hallazgo en el título; overplotting y colas largas tratados cuando aparecen; cada gráfico se interpreta por lo que muestra (17 a 20 pts) | Gráficos correctos pero con rótulos incompletos o sin interpretación; saturación o colas largas sin tratar (9 a 16 pts) | Gráficos ilegibles, sin rótulos o ausentes (0 a 8 pts) | 20 |
| 5. Hallazgos, código y reproducibilidad | El notebook corre de principio a fin; código legible con NumPy, Pandas y Matplotlib; cierra con 3 a 5 hallazgos en frases completas y el modelo que se imagina ajustar (13 a 15 pts) | Corre con ajustes menores, o los hallazgos son una lista de números sin lectura (7 a 12 pts) | El notebook no corre, o no hay síntesis de hallazgos (0 a 6 pts) | 15 |

Puntaje total: 100 puntos. La nota se calcula de forma lineal sobre el puntaje;
la calificación mínima de aprobación del módulo es 60%.

Sobre la ponderación: si sus datos traen factores de expansión o pesos de
muestreo, los análisis que hablen de la población deben usarlos, como se
trabajó en las clases 2 a 4. Si no los traen, no corresponde inventarlos.

## Uso de inteligencia artificial

Se aplica la regla del módulo: el uso de IA generativa está permitido con
declaración (qué herramienta se usó y para qué). Debe entender y poder explicar
cualquier parte de lo que entregue.
