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

## Etapa 1: una respuesta que es sí o no (slides 5 a 8)

La variable respuesta y vale 1 (sí) o 0 (no), y hay una o más variables x con
las que explicarla (slide 6). Un cliente tomado al azar es una **Bernoulli**:
sí con probabilidad p, no con probabilidad 1 − p. La media de una columna de
ceros y unos es la fracción de unos, la **proporción**: en los clientes,
p = 0,033, porque 333 de 10.000 dejaron de pagar (slides 7 y 8). Contar los
síes entre n clientes es la binomial de la clase 5.

Un dato que importa al final: el sí es raro (3,3%).

## Etapa 2: la recta no sirve (slides 9 a 11)

**De dónde salen las probabilidades** (slide 10). Se agrupan los clientes por
**tramo** de deuda, un intervalo de 300 dólares (0 a 300, 300 a 600, y así
hasta 2.700: nueve tramos), y en cada tramo se cuenta cuántos clientes hay y
cuántos dejaron de pagar. En el tramo de 1.800 a 2.100 dólares hay 229
clientes y 114 dejaron de pagar: 114 / 229 = 0,50. Esa fracción es la
probabilidad de no pagar de un cliente con esa deuda, estimada con los datos,
y es un punto del gráfico: nueve tramos, nueve puntos, que suben en forma de
S: casi 0 con deudas bajas, 0,50 entre 1.800 y 2.100 dólares, 1 desde los
2.400.

**La recta** (slide 11). Si se ajusta la recta de mínimos cuadrados con la
respuesta 0/1, la recta intenta ser una probabilidad y no lo logra: con deuda
0 predice −0,08, una probabilidad negativa, y con 2.000 dólares predice 0,18
cuando en ese tramo la mitad de los clientes no paga. Una probabilidad vive
entre 0 y 1 y, en los datos, sube en forma de S. La recta no respeta ni el
rango ni la forma.

## Etapa 3: la regresión logística (slides 12 a 17)

**La sigmoide** (slide 13) es una función que toma cualquier número z y
devuelve un número entre 0 y 1: en z = 0 vale 0,5, hacia la derecha se acerca
a 1 y hacia la izquierda a 0, sin pasarse nunca. La **regresión logística**
(slide 14) pasa la recta de siempre por esa función:

    P(y = 1 | x) = 1 / (1 + e^(−(a + b·x)))

donde P(y = 1 | x) es la probabilidad de un sí dado x, y a + b·x es la recta.
La misma ecuación, despejada, dice que la recta es el logaritmo de las
**chances** (en inglés, odds), la razón sí contra no:

    log(P / (1 − P)) = a + b·x

Con P = 0,8 las chances son 0,8 / 0,2 = 4: cuatro síes por cada no. Como la
recta está en escala de logaritmo, **e^b dice cuánto se multiplican las
chances por cada unidad de x**, igual que en el modelo en log de la clase 4.

**Cómo se lee b** (slide 15). Con la deuda en cientos de dólares, b = 0,55 y
e^b = 1,73: cada 100 dólares más de deuda multiplican las chances de no pagar
por 1,7. En probabilidades: 0,01 con 1.000 dólares, 0,08 con 1.500, 0,59 con
2.000. La curva cruza 0,5 en 1.937 dólares.

**Cómo se ajusta** (slide 16). No por mínimos cuadrados, porque con un 0/1 no
hay una distancia vertical con sentido, sino por **máxima verosimilitud**: se
eligen los a y b que hacen más probable haber observado exactamente estos síes
y noes. statsmodels lo resuelve por iteraciones; en el notebook, `smf.logit`
con la misma sintaxis de fórmulas que `smf.ols` (slide 17), y `predict`
entrega probabilidades.

## Etapa 4: el mismo summary (slides 18 a 24)

El summary tiene las columnas de la clase 5: coeficiente, error estándar (EE),
z, valor p e intervalo (slide 19). La única diferencia es z en lugar de t: con
muchos datos la referencia es la normal en vez de la t de Student, y P>|z| se
lee igual que P>|t|.

**Varias variables** (slides 20 y 21). Solos, los estudiantes dejan de pagar
más (4,3% contra 2,9%). Pero los estudiantes deben más (deuda media 988
dólares contra 772), y a igual deuda dejan de pagar menos. Al poner la deuda en
el modelo, el coeficiente de estudiante cambia de signo: e^(−0,65) = 0,52, a
igual deuda e ingreso las chances de un estudiante son la mitad. Es la
confusión de variables de la clase 4, ahora en la logística; `estudiante` es
una dummy, como lo era el modo de transporte. El ingreso no aporta (p = 0,71):
con la deuda en el modelo no dice nada nuevo.

**El Titanic** (slides 22 a 24). 891 pasajeros; el 74% de las mujeres
sobrevivió contra el 19% de los hombres, y la clase del pasaje ordena a ambos
grupos. El modelo usa el sexo, la clase (categórica, con dummies) y la edad,
que falta en 177 pasajeros. Cada e^b compara con una referencia, a igualdad de
las otras variables: las chances de sobrevivir de una mujer son 12 veces las
de un hombre (e^2,52); las de la tercera clase, el 8% de las de la primera
(e^−2,58); cada año de edad las multiplica por 0,96. Con varias variables, la
recta suma el aporte de cada una y la sigmoide da la probabilidad: 0,94 para
una mujer de primera clase de 30 años, 0,08 para un hombre de tercera de la
misma edad.

## Etapa 5: clasificar (slides 25 a 31)

**El umbral** (slide 26). Un clasificador convierte la probabilidad en un sí
o un no con un umbral; el más simple es 0,5. Con él, el modelo dice "no paga"
desde los 1.937 dólares de deuda.

**La matriz de confusión** (slide 27) cruza lo real (filas) con lo predicho
(columnas). La diagonal son los aciertos: verdaderos positivos y verdaderos
negativos. Fuera de ella, los dos errores:

- **Falso negativo**: era sí y el modelo dijo no. Un cliente que no pagará y
  recibió la tarjeta (233 en el ejemplo).
- **Falso positivo**: era no y el modelo dijo sí. Un cliente que sí pagaba y a
  quien se le negó (42 en el ejemplo).

Los dos errores no cuestan lo mismo, y cuál cuesta más lo dice el problema,
no el modelo (slide 28): para el banco, el falso negativo es dinero perdido y
el falso positivo, un cliente perdido; para un filtro de correo, el falso
positivo es un mensaje real en la carpeta de spam; para un examen médico, el
falso negativo es una enfermedad sin detectar. Cómo elegir el umbral según
ese costo queda para la próxima clase.

**La exactitud engaña cuando el sí es raro** (slide 29). La exactitud es la
fracción de aciertos: el modelo acierta el 97,3%, pero decir que nadie deja de
pagar acierta el 96,7%. De los 333 clientes que no pagan, el modelo detecta
100. Con un sí raro, la exactitud mide sobre todo lo fácil: los noes.

**Lo que queda para la próxima clase.** Dos medidas que salen de la misma
matriz y no engañan cuando el sí es raro (sensibilidad y especificidad), cómo
elegir el umbral según el costo de cada error, y la curva ROC, se ven el
martes 15.

**El Titanic como clasificador** (slide 30). Con un sí frecuente (41%), la
exactitud sí informa: 79% contra el 59% de decir que todos murieron. Los
errores: 83 falsos negativos (pasajeros que sobrevivieron y el modelo daba por
muertos) y 68 falsos positivos.

**Evaluar fuera de la muestra** (slide 31). Medir la exactitud en los mismos
datos con que se ajustó el modelo es hacer trampa: el modelo ya los vio. Se
separa al azar una parte de **prueba** antes de ajustar; el modelo se ajusta
solo con la parte de **entrenamiento** y se mide en la de prueba. Con modelos
simples como los de hoy las dos cifras se parecen; con modelos más flexibles
la de entrenamiento sube y la de prueba no, y la de prueba es la única que
vale. Es el punto de partida de la evaluación de modelos en el resto del
diplomado.

## La respuesta a la pregunta de la clase (slides 32 y 33)

El modelo no dice quién deja de pagar ni quién sobrevivió: dice con qué
probabilidad. El sí o el no lo ponemos nosotros con el umbral, y cada umbral
deja una cantidad de falsos positivos y de falsos negativos. La
exactitud sola no basta: hay que mirar los dos errores por separado, y
medirlos en datos que el modelo no vio.

## En el notebook

| Sección | Qué se hace |
|---|---|
| 2 | La proporción, la binomial y la fracción que no paga por tramo de deuda. |
| 3 | La recta sobre el 0/1 y sus predicciones fuera de rango. |
| 4 | `smf.logit`, e^b, `predict`, la curva, el summary y el intervalo de e^b. |
| 5 | El estudiante con y sin la deuda; el Titanic con `C(clase)`; los perfiles. |
| 6 | El umbral 0,5, la matriz de confusión con `pd.crosstab`, los dos errores, la exactitud contra la base y el Titanic como clasificador. |
| 7 | Reparto entrenamiento y prueba, y la exactitud en cada parte. |

## Glosario

- **Bernoulli**: variable que vale 1 con probabilidad p y 0 con probabilidad 1 − p.
- **Proporción**: la media de una columna de ceros y unos; la fracción de síes.
- **Sigmoide**: función que convierte cualquier número en una probabilidad entre 0 y 1.
- **Chances (odds)**: P / (1 − P), la razón sí contra no.
- **e^b**: cuánto se multiplican las chances por cada unidad de x.
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
