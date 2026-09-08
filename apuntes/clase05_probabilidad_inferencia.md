# Clase 5: probabilidad e inferencia. Guía de lectura de las slides

Diplomado en Ciencia de Datos Aplicada, Módulo 1: Introducción y fundamentos
estadísticos. Esta guía acompaña las slides de la clase 5
(`presentaciones/clase05_probabilidad_inferencia.pdf`) y el notebook
`05_probabilidad_inferencia.ipynb`. Sigue el orden de las slides, indica el
número de cada una y explica con palabras lo que en la clase se dijo en voz
alta. Los números son los de los datos de la clase: la Encuesta Origen Destino
de Santiago (EOD 2012), con 113.113 viajes y 45 comunas.

## El hilo de la clase

Toda la clase cabe en una frase: **todo número que sale de una muestra se
mueve de muestra en muestra; el error estándar mide cuánto, y se usa de dos
formas**. La primera forma es el intervalo de confianza, que convierte el error
estándar en un rango. La segunda es la prueba de hipótesis, que lo usa para
decidir si un resultado es real o azar. Las cinco etapas de la clase recorren
esa idea primero con la media de la duración de los viajes, donde el
movimiento se puede ver porque tenemos la población, y después con la
pendiente de la regresión de las comunas, donde se ve remuestreando.

La pregunta que la clase responde viene de la clase 3 (slide 4): la recta que
relaciona la duración media del viaje con el ingreso medio de la comuna tiene
pendiente −4,8 minutos por millón de pesos, calculada con 45 comunas. ¿Esa
pendiente es real, o es el azar de qué comunas y qué viajes cayeron en la
encuesta?

## Apertura: descriptiva e inferencia (slides 1 a 5)

En las clases 2 a 4 hicimos **estadística descriptiva**: resumir y graficar la
tabla que tenemos. Sus números (media, dispersión, correlación, la recta)
hablan solo de esas filas. La **inferencia estadística** usa los mismos datos
para hablar de la población de la que salió la tabla, y dice cuánta
incertidumbre trae esa afirmación (slide 5). Hace dos preguntas: ¿cuánto vale?
(estimación, con un intervalo) y ¿es real o azar? (prueba de hipótesis, con
un valor p). Para hablar de incertidumbre se necesita el lenguaje de la
probabilidad; por eso la clase parte por ahí.

## Etapa 1. El azar tiene forma (slides 6 a 10)

Una **variable aleatoria** es una cantidad cuyo valor depende del azar: la
duración del próximo viaje que registre la encuesta puede ser 10 minutos o
90. Su **distribución** dice qué valores toma y con qué frecuencia; para la
población completa, es el histograma. La esperanza es su media, 36,9 minutos
(slide 7).

La observación clave de la etapa está en la slide 8: **la media de una muestra
también es una variable aleatoria**. Si tomamos 100 viajes al azar y
calculamos su media, obtenemos un número; con otros 100 viajes, otro número.
La duración de un viaje no tiene forma de campana (cola larga hacia los
viajes largos), pero las medias de muchas muestras de 100 viajes sí la tienen.

Esa campana se llama **distribución normal** (slide 9). Tiene dos parámetros:
μ, la media, el centro de la campana, y σ, la desviación estándar, su ancho.
Su regla práctica: el 68% de los valores cae a menos de una σ de la media, el
95% a menos de 1,96 σ, y el 99,7% a menos de 3 σ. El 1,96 reaparece en toda
la clase.

Los datos crudos no necesitan ser normales. La duración en minutos no lo es
(asimetría 5,3); en logaritmo se parece bastante (slide 10), y esa es la razón
de fondo del log que usamos en la clase 4. Lo que la inferencia necesita es
que los promedios sean normales, y eso lo garantiza el teorema de la etapa 2.

## Etapa 2. Un número se mueve (slides 11 a 16)

Para ver el movimiento, la clase trata los 113.113 viajes de la EOD como si
fueran la población y saca muestras de 100 viajes muchas veces. Dos muestras
dan dos medias distintas (slide 12). Dos mil muestras dan un histograma de
medias: la **distribución muestral** de la media, centrada en la media real
(slide 13). Su desviación estándar se llama **error estándar**: cuánto se
mueve la media de una muestra a otra.

Dos cosas se confunden porque tienen el mismo nombre (slide 14):

- La **desviación estándar** describe los datos: cuánto varía la duración de un
  viaje a otro. Para la población, σ = 36,0 minutos.
- El **error estándar** describe el estimador: cuánto varía la media de una
  muestra a otra. Es la desviación estándar de la distribución muestral,
  3,6 minutos, y por eso es mucho más chico.

En la vida real no hay 2.000 muestras ni población a la vista: hay una sola
muestra. La fórmula da el mismo número desde ella (slide 15):

    EE(x̄) = σ / √n ≈ s / √n

donde x̄ es la media de la muestra, σ la desviación estándar de la duración en
la población, s la misma desviación estándar pero calculada en la única
muestra que se tiene, y n el tamaño de la muestra. Con n = 100: 36,0 / 10 =
3,6 por la fórmula con σ, y 35,1 / 10 = 3,5 con la s de una muestra. La
decisión de reemplazar σ por s tiene una consecuencia pequeña que aparece en
la etapa 5 (la t de Student).

El **teorema central del límite** (slide 16) dice que la media de una muestra
se distribuye aproximadamente normal alrededor de la media real, con
desviación σ/√n, aunque la variable original no sea normal. Con muestras de
30, 100 y 500 viajes, el error estándar baja de 6,6 a 3,7 y 1,6: para
reducirlo a la mitad hay que cuadruplicar la muestra.

## Etapa 3. Primer uso del error estándar: el intervalo (slides 17 a 20)

El intervalo sale de dos pasos (slide 18). Paso 1: como las medias muestrales
son normales, el 95% de ellas cae a menos de 1,96 errores estándar de la media
real. Paso 2 es la misma frase al revés: la media real está a menos de 1,96
errores estándar de la media de mi muestra, en el 95% de las muestras. Ese
rango es el **intervalo de confianza del 95%** (slide 19):

    x̄ ± 1,96 · s / √n

Se lee sobre el procedimiento, no sobre un intervalo en particular: si
repitiéramos el muestreo muchas veces, el 95% de los intervalos atraparía la
media real. Este intervalo la atrapa o no, y nunca sabremos cuál de las dos.
La slide 20 lo comprueba con la población: de 100 intervalos, cerca de 95
atrapan la media real.

## Etapa 4. La pendiente también se mueve (slides 21 a 33)

La pendiente de la recta duración = a + b · ingreso es el coeficiente del
ingreso en el summary de statsmodels: b = −4,8 minutos por millón de pesos.
Es un número que salió de una muestra de 45 comunas; con otras comunas
saldría otra b. El problema es que no hay una población de comunas de donde
sacar otra muestra (slide 21).

El **bootstrap** (Efron y Tibshirani, 1993) trata la muestra como si fuera la
población y saca de ella muchas muestras nuevas del mismo tamaño, **con
reemplazo** (slide 22). Los cinco pasos: tomar las 45 comunas; sacar una al
azar, anotarla y devolverla a la bolsa, de modo que pueda volver a salir;
repetir 45 veces, lo que da una remuestra con algunas comunas repetidas y
otras ausentes; ajustar la recta y guardar su pendiente; repetir los pasos
2 a 4 dos mil veces. Sacar con reemplazo no es quitar una comuna y poner
otra; es devolver la comuna sacada antes de sacar la siguiente. Sin reemplazo
no serviría: 45 de 45 son siempre las mismas 45 comunas y la misma recta.

La slide 23 muestra una remuestra concreta: 15 comunas no salieron, 18
salieron una vez, 12 dos veces o más (una salió cuatro veces), y la recta de
esa remuestra tiene pendiente −6,1 en lugar de −4,8. Con 30 remuestras hay 30
rectas y 30 pendientes (slide 24). ¿Cómo hay tantas combinaciones si solo hay
45 puntos? Con tres comunas A, B y C, sacar tres con reemplazo da diez
remuestras distintas (AAA, AAB, AAC, ABB, ABC, ACC, BBB, BBC, BCC, CCC), y
siete rectas distintas (slide 25). Con 45 comunas las combinaciones son del
orden de 5 × 10²⁵. De las 2.000 remuestras que hace el código, las 2.000 son
distintas entre sí; se usan 2.000 porque desde ahí el error estándar deja de
cambiar (slide 26). Lo que se repite es el procedimiento, no el ajuste.

El código (slide 27) cabe en cinco líneas: `rng.integers(0, 45, 45)` saca 45
índices con repetición, `np.polyfit` ajusta la recta, y `np.percentile` con
2,5 y 97,5 da el intervalo. Las 2.000 pendientes forman una campana alrededor
de la observada (slide 28); su desviación, 1,82, es el **error estándar de la
pendiente**, el mismo concepto que el de la media. El **intervalo bootstrap**
(slide 29) se lee directo del histograma: ordenar las 2.000 pendientes, tomar
la número 50 desde abajo (percentil 2,5, −9,1) y la número 50 desde arriba
(percentil 97,5, −2,1); entre ambas queda el 95% central. No supone forma de
campana.

statsmodels no remuestrea: calcula el error estándar de la pendiente con una
fórmula, a partir de los residuos (slides 30 y 31):

    EE(b) = s / √Σ(xᵢ − x̄)²,   con   s = √(Σeᵢ² / (n − 2))

donde eᵢ es el residuo de la comuna i (su distancia vertical a la recta), s es
la desviación de esos residuos y reemplaza a σ, la desviación de los errores
alrededor de la recta verdadera, que no se conoce; xᵢ − x̄ es cuánto se aleja
el ingreso medio de cada comuna del ingreso medio de todas, y n − 2 son las 45
comunas menos los dos parámetros de la recta. Con las comunas: s = 5,5 minutos
y √Σ(xᵢ − x̄)² = 2,73, así que EE(b) = 5,5 / 2,73 = 2,02, la columna std err
del summary. La pendiente se mueve menos cuando las comunas están cerca de la
recta (s chico) y cuando los ingresos están bien desplegados.

El intervalo de la pendiente por la fórmula es b ± 2,02 · EE = [−8,9; −0,75],
las columnas 0,025 y 0,975 del summary (slide 32). La tabla de la slide 33
compara los dos caminos: se parecen, y ningún intervalo incluye el 0. La
fórmula es instantánea, pero existe solo para algunos estadísticos y supone
cosas sobre los residuos; el bootstrap sirve para cualquier estadístico y solo
pide que la muestra represente a la población.

## Etapa 5. Segundo uso del error estándar: el contraste (slides 34 a 44)

**Qué tiene que ver el valor p con la regresión** (slide 35). La recta resume
45 puntos, y esos puntos son una muestra. Imaginemos el mundo donde no hay
relación entre ingreso y duración: la pendiente real es 0. Incluso en ese
mundo, por el azar de qué hogares cayeron en la encuesta, la recta ajustada
tendría alguna pendiente. ¿Cuán grande? El error estándar dice cuánto suele
inclinarla el azar: por la regla del 95% de la normal, casi todas las
pendientes de puro azar quedan a menos de 2 errores estándar de cero, es
decir, entre −4 y +4. Nuestra pendiente está a 2,4 errores estándar del cero.
El **valor p** es la probabilidad de que el azar produzca una pendiente tan
lejos de cero como la nuestra, si la pendiente real fuera 0: el 2,1% de las
veces. Es demasiado raro para atribuirlo al azar, y por eso concluimos que la
relación probablemente es real. Si p hubiera dado 0,40, el azar produciría
pendientes así el 40% de las veces y no podríamos distinguir la recta del
ruido; no habría evidencia, que no es lo mismo que no exista.

La slide 36 muestra la misma campana en dos posiciones. Centrada en lo
observado, −4,8, responde cuánto se mueve nuestra pendiente y da el
intervalo. Centrada en 0, responde qué haría el azar si no hubiera relación y
da la prueba; más allá de ±4,1 está la zona donde se rechaza la hipótesis
nula. Que el intervalo no toque el 0 y que −4,8 caiga en la zona de rechazo
es la misma afirmación.

Con nombres (slide 37): la **hipótesis nula** H0 es que la pendiente real es
0, el ingreso no tiene efecto; la **alternativa** H1, que no lo es. El
estadístico es t = b / EE(b), a cuántos errores estándar del cero está la
pendiente: −4,81 / 2,02 = −2,39 (slide 38). El valor p es la probabilidad, si
H0 fuera cierta, de un t así de lejos de cero por cualquiera de los dos lados.
La convención es rechazar H0 cuando p < 0,05. El cálculo (slide 39):

    p = 2 · (1 − F(|t|))

donde F es la función acumulada de la **t de Student** con n − 2 = 43 grados
de libertad, y el 2 cuenta las dos colas. En Python:
`p = 2 * (1 - stats.t.cdf(abs(t), df=43))`, que da 0,021. La t de Student es
la normal con un margen extra, porque σ se estimó con s a partir de pocos
datos; con 45 comunas el 1,96 se vuelve 2,02, y con muchos datos vuelve a ser
la normal. statsmodels la usa sola.

Con eso el summary se lee completo (slide 40): coef, std err, t, P>|t| y el
intervalo. La respuesta a la pregunta de la clase (slide 41): la pendiente
que nos dio el modelo no es azar. En las comunas de mayor ingreso los viajes
duran menos, unos 4,8 minutos menos por cada millón de pesos de ingreso medio,
entre 0,75 y 8,9. Tres advertencias: con 45 comunas el resultado apenas cruza
el umbral, porque el valor p depende del tamaño del efecto y del tamaño de la
muestra; que un efecto sea estadísticamente significativo no dice que sea
grande, el tamaño lo da el coeficiente y su precisión el intervalo; y
correlación no es causalidad, tampoco con p pequeño.

**Lo que suponen esos t y p** (slides 42 a 44). No que las variables sean
normales. Los supuestos son sobre los residuos:

1. **Independientes**: el residuo de un viaje no debería decir nada del
   residuo de otro. En la EOD la vuelta se parece a la ida (correlación 0,63
   entre los residuos de los dos primeros viajes de una misma persona, contra
   0,00 entre viajes de personas distintas). statsmodels cuenta 102 mil viajes
   independientes cuando hay menos información, y el error estándar queda
   demasiado chico.
2. **Misma varianza en todo el rango**: la dispersión de los residuos del
   modelo duración contra distancia crece de 17 a 45 minutos con la distancia;
   en log cambia mucho menos. Otra razón del log de la clase 4.
3. **Normales**: importa con pocos datos, como las 45 comunas, donde conviene
   mirar el histograma de residuos y los atípicos. Con 18 mil hogares deja de
   importar: los residuos del modelo de motorización no son normales y su
   pendiente igual se reparte como una normal, por el teorema central del
   límite.

## Para practicar con el notebook

El notebook sigue el mismo orden: sección 2, el azar tiene forma; sección 3,
la distribución muestral y el error estándar; sección 4, el intervalo;
sección 5, la pendiente y el bootstrap; sección 6, la prueba de hipótesis y
los supuestos; sección 7, el ejercicio con los datos de su proyecto.

## Glosario

- **Variable aleatoria**: cantidad cuyo valor depende del azar. Su
  distribución dice qué valores toma y con qué frecuencia.
- **σ y s**: la desviación estándar de una variable en la población (σ) y en
  la muestra (s). Miden lo mismo, cuánto varía la variable de un caso a otro.
- **Distribución muestral**: la distribución de un estadístico (la media, la
  pendiente) a través de muchas muestras.
- **Error estándar (EE)**: la desviación estándar de la distribución muestral;
  cuánto se mueve el estadístico de una muestra a otra.
- **Intervalo de confianza del 95%**: estimación ± 1,96 · EE (2,02 · EE con la t
  de 43 grados de libertad); atrapa el valor real en el 95% de las muestras.
- **Bootstrap**: remuestrear la muestra con reemplazo para estimar la
  distribución muestral de un estadístico.
- **b**: la pendiente de la recta; el coeficiente de la variable en el summary.
- **t**: b / EE(b), a cuántos errores estándar del cero está el coeficiente.
- **Valor p**: la probabilidad de un t tan lejos de cero como el observado, si
  el efecto real fuera cero.
- **H0 y H1**: la hipótesis nula (no hay efecto) y la alternativa.
- **t de Student**: la distribución de t cuando σ se estimó con s; la normal
  con un margen extra que depende de los grados de libertad, n − 2 para una
  recta.

## Referencias

- Efron, B. y Tibshirani, R. (1993). *An Introduction to the Bootstrap*.
  Chapman and Hall.
- Wasserstein, R. y Lazar, N. (2016). The ASA statement on p-values: context,
  process, and purpose. *The American Statistician*, 70(2), 129-133.
- VanderPlas, J. (2016). *Python Data Science Handbook*. O'Reilly (versión en
  línea de acceso abierto).
- Encuesta Origen Destino de Santiago 2012, SECTRA.
