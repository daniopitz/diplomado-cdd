# Clase 6: regresión logística, ¿sí o no?

Guía de lectura de las slides. Módulo 1: Introducción y fundamentos
estadísticos, Diplomado en Ciencia de Datos Aplicada, UTFSM. Jueves 10 de
septiembre de 2026.

Esta guía sigue el orden de las slides y sirve para repasar la clase o para
leerla antes. Los números entre paréntesis son las slides donde aparece cada
idea. El código completo está en el notebook `06_regresion_logistica.ipynb`.

## El hilo de la clase

En las clases 4 y 5 la respuesta era un número (la duración de un viaje) y el
modelo era una recta. Hoy la respuesta es un sí o un no: ¿este cliente dejará
de pagar?, ¿este pasajero sobrevivió? La misma recta sirve, pero hay que
pasarla por una curva. Y hay una idea que ordena toda la clase:

> El modelo no predice el sí o el no: predice una probabilidad. La decisión,
> y sus dos errores, la ponemos nosotros.

Dos ejemplos, ninguno de la EOD: 10.000 clientes de una tarjeta de crédito
(datos del libro de James, Witten, Hastie y Tibshirani), con su deuda en la
tarjeta, es decir, lo que deben después del pago mensual, su ingreso anual y
si son estudiantes; y 891 pasajeros del Titanic.

## Etapa 1: una respuesta que es sí o no (slides 5 a 9)

La variable respuesta y vale 1 (sí) o 0 (no), y hay una o más variables x con
las que explicarla (slide 6). Un cliente tomado al azar es una **Bernoulli**:
sí con probabilidad p, no con probabilidad 1 − p. La media de una columna de
ceros y unos es la fracción de unos, la **proporción**: en los clientes, 333
de 10.000 dejaron de pagar, p = 333 / 10.000 = 0,033, y 1 − p = 0,967
(slides 8 y 9). Es la distribución más simple que existe: dos resultados y una
probabilidad.

Un dato que importa al final: el sí es raro (3,3%).

## Etapa 2: la recta no sirve (slides 10 a 12)

**La probabilidad de no pagar, por tramo de deuda** (slide 11). Se agrupan los clientes por
**tramo** de deuda, un intervalo de 300 dólares (0 a 300, 300 a 600, y así
hasta 2.700: nueve tramos), y en cada tramo se cuenta cuántos clientes hay y
cuántos dejaron de pagar. En el tramo de 1.800 a 2.100 dólares hay 229
clientes y 114 dejaron de pagar: 114 / 229 = 0,50. Esa fracción es la
probabilidad de no pagar de un cliente con esa deuda, estimada con los datos,
y es un punto del gráfico: nueve tramos, nueve puntos, que suben en forma de
S: casi 0 con deudas bajas, 0,50 entre 1.800 y 2.100 dólares, 1 desde los
2.400.

**La recta** (slide 12). Si se ajusta la recta de mínimos cuadrados de la clase
4 con la respuesta 0/1, lo que predice para cada deuda es el promedio de y
entre los clientes con esa deuda, y el promedio de una columna de ceros y
unos es la fracción de unos: la recta predice la fracción que no paga según
la deuda, la misma cantidad que las fracciones por tramo estiman sin modelo,
y por eso se pueden comparar. La recta intenta ser una probabilidad y no lo
logra:
con deuda 0 predice −0,08, una probabilidad negativa, y con 2.000 dólares
predice 0,18 cuando la fracción real de ese tramo es 0,50. Una probabilidad
vive entre 0 y 1 y las fracciones suben en forma de S; la recta no respeta ni
el rango ni la forma. La curva que sí lo hace es la regresión logística.

## Etapa 3: la regresión logística (slides 13 a 21)

La idea central de esta etapa: la regresión logística no inventa una curva.
Pone la recta de siempre en una escala donde no puede salirse de rango, y la
S es cómo se ve esa recta al volver a las probabilidades. Se construye en dos
pasos.

**Los odds (chances)** (slide 14). Son la probabilidad dicha de otra forma: cuántos
síes hay por cada no, odds = P / (1 − P). Con P = 0,8, de cada 10 clientes
8 no pagan y 2 pagan: odds 8 / 2 = 4, cuatro a uno. Con P = 0,5, uno a uno.
Con P = 0,2, 0,25, uno a cuatro. Los odds van de 0 a infinito: ya no tienen
el techo de 1, pero no pueden ser negativas.

**Despejar P** (slide 15). El modelo dice que el logaritmo de los odds es la
recta, z = a + b·x. El logaritmo de los odds puede ser cualquier número,
positivo o negativo (log(4) = 1,39, log(1) = 0, log(0,25) = −1,39): sin techo
ni piso, ahí sí cabe una recta. Para volver a la probabilidad se despeja P en cuatro
pasos: log(P / (1 − P)) = z; P / (1 − P) = e^z; P = e^z (1 − P), es decir
P (1 + e^z) = e^z; y P = e^z / (1 + e^z) = 1 / (1 + e^(−z)). Ese resultado es
la sigmoide: no se eligió aparte, salió de despejar P, y por eso el exponente
es la recta.

**La misma relación en tres escalas** (slide 16). Con los nueve tramos de la
slide 11: en odds, los puntos suben como una exponencial; en logaritmo de los
odds, siguen una recta, y eso es lo que el modelo supone; en probabilidad,
la S. La recta y la S son la misma relación vista en dos escalas.

**La fórmula** (slide 17). El modelo es:

    log(P / (1 − P)) = a + b·x

donde P es la probabilidad de un sí dado x, P / (1 − P) son los odds, y
a + b·x es la recta. Despejando P (se toma e a ambos lados y se ordena) queda:

    P(y = 1 | x) = 1 / (1 + e^(−(a + b·x)))

Por eso el exponente es a + b·x: es la recta del modelo, que reaparece al
despejar. Y como sumar b en el logaritmo es multiplicar afuera por e^b, **e^b
dice cuánto se multiplican los odds por cada unidad de x**, igual que en el
modelo en log de la clase 4.

**La sigmoide** (slide 19) es la función que apareció al despejar: toma el
logaritmo de los odds z, cualquier número, y devuelve la probabilidad, entre
0 y 1. En z = 0 (odds uno a uno) vale 0,5; hacia la derecha se acerca a 1 y
hacia la izquierda a 0, sin pasarse nunca.

**Cómo se lee b** (slide 20). Con la deuda en cientos de dólares, b = 0,55 y
e^b = 1,73: cada 100 dólares más de deuda multiplican los odds de no pagar
por 1,7. En probabilidades: 0,01 con 1.000 dólares, 0,08 con 1.500, 0,59 con
2.000. La curva cruza 0,5 en 1.937 dólares.

**En el notebook**, `smf.logit` tiene la misma sintaxis de fórmulas que `smf.ols`
(slide 21), y `predict` entrega probabilidades. El ajuste no es por mínimos
cuadrados sino por máxima verosimilitud, que statsmodels resuelve por
iteraciones; el detalle queda para el notebook.

## Etapa 4: el mismo summary (slides 22 a 33)

El summary tiene las columnas de la clase 5: coeficiente, error estándar (EE),
z, valor p e intervalo (slide 23). La única diferencia es z en lugar de t: con
muchos datos la referencia es la normal en vez de la t de Student, y P>|z| se
lee igual que P>|t|.

**Varias variables** (slides 24 a 27). Solos, los estudiantes dejan de pagar
más (4,3% contra 2,9%). Pero los estudiantes deben más (deuda media 988
dólares contra 772), y a igual deuda dejan de pagar menos. Al poner la deuda en
el modelo, el coeficiente de estudiante cambia de signo: e^(−0,65) = 0,52, a
igual deuda e ingreso los odds de un estudiante son la mitad. Es la
confusión de variables de la clase 4, ahora en la logística; `estudiante` es
una dummy, como lo era el modo de transporte. El ingreso no aporta (p = 0,71):
con la deuda en el modelo no dice nada nuevo.

**El modelo final de los clientes, escrito** (slide 28): deuda y estudiante,
porque el ingreso no aporta:

    log(P / (1 − P)) = −10,75 + 0,57·deuda₁₀₀ − 0,71·estudiante

donde deuda₁₀₀ es la deuda en cientos de dólares y estudiante vale 1 o 0; P
sale de la sigmoide, P = 1 / (1 + e^(−z)) con z la recta. Un estudiante con
2.000 dólares de deuda: z = −10,75 + 0,57·20 − 0,71 = 0,01, P = 0,50; un no
estudiante con la misma deuda: z = 0,73, P = 0,67.

El mecanismo, con un ejemplo inventado de 200 clientes:

| | no estudiantes | estudiantes |
|---|---|---|
| deuda baja | 80 clientes, 4 no pagan (5%) | 20 clientes, 0 no pagan (0%) |
| deuda alta | 20 clientes, 10 no pagan (50%) | 80 clientes, 32 no pagan (40%) |
| total | 100 clientes, 14 no pagan (14%) | 100 clientes, 32 no pagan (32%) |

Dentro de cada tramo los estudiantes pagan mejor, pero 80 de los 100
estudiantes están en el tramo de deuda alta y solo 20 de los 100 no
estudiantes, así que en el total parecen peores. El modelo con solo
`estudiante` lee el total; el modelo con la deuda compara dentro de cada
tramo. Ninguno se equivoca en la aritmética: responden preguntas distintas, y
la segunda es la que interesa.

**El Titanic** (slides 29 a 33). 891 pasajeros; el 74% de las mujeres
sobrevivió contra el 19% de los hombres, y la clase del pasaje ordena a ambos
grupos. El modelo usa el sexo, la clase (categórica, con dummies) y la edad,
que falta en 177 pasajeros. Cada e^b compara con una referencia, a igualdad de
las otras variables: los odds de sobrevivir de una mujer son 12 veces las
de un hombre (e^2,52); las de la tercera clase, el 8% de las de la primera
(e^−2,58); cada año de edad las multiplica por 0,96. Con varias variables, la
recta suma el aporte de cada una y la sigmoide da la probabilidad: 0,94 para
una mujer de primera clase de 30 años, 0,08 para un hombre de tercera de la
misma edad.

**El modelo del Titanic, escrito** (slide 32):

    log(P / (1 − P)) = 1,25 + 2,52·mujer − 1,31·clase2 − 2,58·clase3 − 0,037·edad

donde mujer vale 1 para las mujeres y 0 para los hombres (la referencia), y
clase2 y clase3 valen 1 en segunda y tercera clase y las dos valen 0 en
primera (la referencia). Una mujer de primera clase de 30 años: z = 1,25 +
2,52 − 0,037·30 = 2,7, P = 0,93.

## Etapa 5: clasificar (slides 34 a 41)

**El umbral** (slide 35). Un clasificador convierte la probabilidad en un sí
o un no con un umbral; el más simple es 0,5. Con él, el modelo dice "no paga"
desde los 1.937 dólares de deuda.

**La matriz de confusión** (slide 36) cruza lo real (filas) con lo predicho
(columnas). La diagonal son los aciertos: verdaderos positivos y verdaderos
negativos. Fuera de ella, los dos errores:

- **Falso negativo**: era sí y el modelo dijo no. Un cliente que no pagará y
  recibió la tarjeta (233 en el ejemplo).
- **Falso positivo**: era no y el modelo dijo sí. Un cliente que sí pagaba y a
  quien se le negó (42 en el ejemplo).

Los dos errores no cuestan lo mismo, y cuál cuesta más lo dice el problema,
no el modelo (slide 37): para el banco, el falso negativo es dinero perdido y
el falso positivo, un cliente perdido; para un filtro de correo, el falso
positivo es un mensaje real en la carpeta de spam; para un examen médico, el
falso negativo es una enfermedad sin detectar. Cómo elegir el umbral según
ese costo queda para la próxima clase.

**La exactitud** (slide 38) es la fracción de aciertos: la diagonal de la
matriz dividida por el total, (VP + VN) / n = (100 + 9.625) / 10.000 = 0,973.
Hay que compararla con la **base**, la exactitud de no tener modelo y predecir
siempre la clase más frecuente: decir que todos pagan acierta 9.667 / 10.000
= 0,967.

**La exactitud engaña cuando el sí es raro** (slide 39). Comparadas: el modelo acierta el 97,3%, pero decir que nadie deja de
pagar acierta el 96,7%. De los 333 clientes que no pagan, el modelo detecta
100. Con un sí raro, la exactitud mide sobre todo lo fácil: los noes.

**Lo que queda para la próxima clase.** Dos medidas que salen de la misma
matriz y no engañan cuando el sí es raro (sensibilidad y especificidad), cómo
elegir el umbral según el costo de cada error, y la curva ROC, se ven el
martes 15.

**El Titanic como clasificador** (slide 40). Con un sí frecuente (41%), la
exactitud sí informa: 79% contra el 59% de decir que todos murieron. Los
errores: 83 falsos negativos (pasajeros que sobrevivieron y el modelo daba por
muertos) y 68 falsos positivos.

**Evaluar fuera de la muestra** (slide 41). Medir la exactitud en los mismos
datos con que se ajustó el modelo es hacer trampa: el modelo ya los vio. Se
separa al azar una parte de **prueba** antes de ajustar; el modelo se ajusta
solo con la parte de **entrenamiento** y se mide en la de prueba. Con modelos
simples como los de hoy las dos cifras se parecen; con modelos más flexibles
la de entrenamiento sube y la de prueba no, y la de prueba es la única que
vale. Es el punto de partida de la evaluación de modelos en el resto del
diplomado.

## La respuesta a la pregunta de la clase (slides 42 y 43)

El modelo no dice quién deja de pagar ni quién sobrevivió: dice con qué
probabilidad. El sí o el no lo ponemos nosotros con el umbral, y cada umbral
deja una cantidad de falsos positivos y de falsos negativos. La
exactitud sola no basta: hay que mirar los dos errores por separado, y
medirlos en datos que el modelo no vio.

## En el notebook

| Sección | Qué se hace |
|---|---|
| 2 | La proporción p. |
| 3 | La fracción que no paga por tramo de deuda: los nueve puntos. |
| 4 | La recta sobre el 0/1: predicciones fuera de rango y lejos de los puntos. |
| 5 | `smf.logit`, e^b, `predict`, la curva, el summary y el intervalo de e^b. |
| 6 | El caso del estudiante paso a paso: el total, la deuda por grupo, la comparación por tramo y los dos modelos; después el ingreso. |
| 7 | Otro problema: el Titanic con `C(clase)` y los perfiles. |
| 8 | El umbral 0,5, la matriz de confusión con `pd.crosstab`, los dos errores, la exactitud contra la base y el Titanic como clasificador. |
| 9 | Reparto entrenamiento y prueba, y la exactitud en cada parte. |

## Glosario

- **Bernoulli**: variable que vale 1 con probabilidad p y 0 con probabilidad 1 − p; la distribución de un sí o no.
- **Proporción**: la media de una columna de ceros y unos; la fracción de síes.
- **Odds (chances)**: P / (1 − P), cuántos síes por cada no; van de 0 a infinito.
- **Logaritmo de los odds (logit)**: la escala en que la logística es una recta; cualquier número, positivo o negativo.
- **Sigmoide**: la función que devuelve la probabilidad a partir del logaritmo de los odds; siempre entre 0 y 1.
- **e^b**: cuánto se multiplican los odds por cada unidad de x.
- **Máxima verosimilitud**: el criterio de ajuste de la logística; elige los coeficientes que hacen más probable lo observado.
- **z**: el t del summary cuando la referencia es la normal; P>|z| se lee igual que P>|t|.
- **Umbral**: la probabilidad a partir de la cual el clasificador dice sí.
- **Matriz de confusión**: la tabla de lo real contra lo predicho.
- **Falso positivo**: el modelo dijo sí y era no. **Falso negativo**: el modelo dijo no y era sí.
- **Exactitud**: fracción de aciertos sobre el total.
- **Entrenamiento y prueba**: la parte de los datos con que se ajusta el modelo y la parte, separada antes, en que se mide.

## Referencias

- James, G., Witten, D., Hastie, T. y Tibshirani, R. (2021). *An Introduction
  to Statistical Learning with Applications in R* (2a ed.). Springer. Capítulo
  4 (regresión logística) y sección 5.1 (conjunto de validación). Disponible
  gratis en [statlearning.com](https://www.statlearning.com).
- Diez, D., Çetinkaya-Rundel, M. y Barr, C. (2019). *OpenIntro Statistics*
  (4a ed.). Sección 9.5 (regresión logística). Disponible gratis en
  [openintro.org](https://www.openintro.org/book/os/).
- Datos: `Default`, del libro de James et al. (statlearning.com), y `Titanic`,
  del repositorio seaborn-data (github.com/mwaskom/seaborn-data). Ambos en
  `datos/clase06/`.
