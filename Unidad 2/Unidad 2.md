# Unidad 2 — Inferencia probabilística y aprendizaje bayesiano

## Teorema de Bayes

### Introducción

En la unidad anterior aprendimos a construir distribuciones de probabilidad a partir de datos observados y a ajustar modelos probabilísticos mediante distribuciones paramétricas.

Sin embargo, en muchos problemas reales no conocemos con certeza cuál es el valor correcto de una probabilidad o de un parámetro. A medida que obtenemos nueva evidencia, nuestras creencias deben modificarse.

La inferencia bayesiana proporciona un marco matemático para realizar esta actualización de conocimiento.

La idea fundamental es sencilla:

> Aprender consiste en modificar probabilidades a partir de nueva evidencia.

---

### El problema de la inferencia

Supongamos que queremos determinar si una moneda es justa.

La probabilidad de obtener cara es:

$$
\theta=P(\text{cara})
$$

Inicialmente desconocemos el valor de $\theta$.

Podríamos preguntarnos:

* ¿Es una moneda justa?
* ¿Está sesgada?
* ¿Qué tan seguros estamos de nuestra respuesta?

La respuesta dependerá de la evidencia observada.

---

### Probabilidad condicional

Recordemos que la probabilidad condicional se define como:

$$
P(A|B)
=
\frac{P(A \cap B)}
{P(B)}
$$

Esta expresión representa la probabilidad de que ocurra el evento (A) cuando sabemos que el evento (B) ya ocurrió.

---

### Derivación del Teorema de Bayes

Podemos escribir:

$$
P(A \cap B)
=
P(A|B)P(B)
$$

y también:

$$
P(A \cap B)
=

P(B|A)P(A)
$$

Igualando ambas expresiones obtenemos:

$$
P(A|B)
=

\frac{P(B|A)P(A)}
{P(B)}
$$

Esta ecuación recibe el nombre de **Teorema de Bayes**.

---

### Interpretación

La ecuación anterior puede leerse como:

```text
Creencia inicial
        ×
Compatibilidad con la evidencia
        ↓
Creencia actualizada
```

o de forma más compacta:

```text
Prior
   ×
Likelihood
   ↓
Posterior
```

---

### Componentes de Bayes

#### Prior

$$
P(A)
$$

Representa nuestra creencia antes de observar la evidencia.

---

#### Likelihood

$$
P(B|A)
$$

Representa qué tan compatible es la evidencia con la hipótesis considerada.

---

#### Evidencia

$$
P(B)
$$

Actúa como constante de normalización.

Garantiza que las probabilidades finales sumen uno.

---

#### Posterior

$$
P(A|B)
$$

Representa nuestra creencia después de observar la evidencia.

Es el resultado final del proceso de aprendizaje.

---

## Aprender como actualización de probabilidades

La interpretación moderna de Bayes consiste en entender el aprendizaje como un proceso continuo de actualización.

Cada nueva observación:

* aporta información,
* elimina hipótesis poco plausibles,
* incrementa la plausibilidad de otras hipótesis.

En lugar de producir respuestas absolutas, Bayes produce distribuciones de probabilidad que reflejan distintos niveles de incertidumbre.

---

## Priors y Posteriors

### Prior

Antes de observar datos tenemos una distribución de creencias.

Por ejemplo, si desconocemos completamente el comportamiento de una moneda, podríamos considerar igualmente plausibles todos los valores:

$$
0 \le \theta \le 1
$$

Una forma de representar esta situación es mediante:

$$
\theta \sim Beta(1,1)
$$

que corresponde a una distribución uniforme.

---

### Posterior

Ahora observamos:

* 8 caras
* 2 sellos

La evidencia sugiere que valores cercanos a:

$$
\theta \approx 0.8
$$

son más plausibles que valores cercanos a 0.2.

La distribución posterior se concentra alrededor de dichos valores.

---

### Mismo valor esperado, distinta incertidumbre

Supongamos dos situaciones:

#### Caso 1

Observamos:

* 1 cara
* 1 sello

Posterior:

$$
Beta(2,2)
$$

---

#### Caso 2

Observamos:

* 100 caras
* 100 sellos

Posterior:

$$
Beta(101,101)
$$

---

En ambos casos la media es aproximadamente:

$$
\theta=0.5
$$

pero la incertidumbre es muy diferente.

La segunda distribución es mucho más concentrada.

Esto ilustra una idea fundamental:

> La evidencia no solamente modifica nuestras probabilidades; también modifica nuestra incertidumbre.

---

## Experimento de Bayes: la moneda izquierda-derecha

### Descripción

Este experimento fue utilizado por Thomas Bayes para ilustrar el proceso de inferencia.

Se coloca una primera moneda aleatoriamente sobre una mesa.

La posición exacta de dicha moneda es desconocida.

Llamaremos:

$$
\theta
$$

a la posición relativa de la moneda medida entre el borde izquierdo y el borde derecho de la mesa.

---

### Incertidumbre inicial

Antes de observar cualquier dato, cualquier posición es igualmente plausible.

Por tanto:

$$
\theta \sim Uniforme(0,1)
$$

La incertidumbre es máxima.

---

### Obtención de evidencia

Posteriormente se lanzan nuevas monedas sobre la mesa.

No observamos su posición exacta.

Únicamente registramos si caen:

* a la izquierda de la moneda original,
* o a la derecha de la moneda original.

Por ejemplo:

```text
L, L, R, L, R, R, L
```

---

### Construcción de evidencia

Si observamos:

* $n_L$ monedas a la izquierda,
* $n_R$ monedas a la derecha,

la probabilidad de observar esos resultados depende de la posición de la moneda original.

---

### Distribución posterior

Puede demostrarse que la distribución posterior es:

$$
\theta
\sim
Beta(n_L+1,;n_R+1)
$$

---

### Interpretación

La posición más probable de la moneda no depende únicamente de la proporción izquierda-derecha.

También depende de la cantidad de observaciones.

Por ejemplo:

#### Caso A

$$
n_L=1
$$

$$
n_R=1
$$

Posterior:

$$
Beta(2,2)
$$

Existe gran incertidumbre.

---

#### Caso B

$$
n_L=100
$$

$$
n_R=100
$$

Posterior:

$$
Beta(101,101)
$$

La media sigue siendo 0.5, pero la incertidumbre es mucho menor.

---

### Relación con el curso

Este experimento resume gran parte de las ideas fundamentales que estudiaremos:

```text
Datos
    ↓
Probabilidades
    ↓
Evidencia
    ↓
Actualización
    ↓
Reducción de incertidumbre
```

La inferencia bayesiana puede interpretarse como un mecanismo matemático para transformar evidencia en conocimiento.

Mira la simulación del experimento de Bayes en el siguiente libro: [Libro Experimento Bayes](./modelo_bayes.ipynb)

---

## Distribución Beta y reducción de incertidumbre

En la sección anterior estudiamos el Teorema de Bayes y observamos cómo una nueva evidencia permite modificar nuestras creencias sobre una hipótesis. Sin embargo, aún no hemos discutido cómo representar matemáticamente la incertidumbre asociada a una probabilidad desconocida.

La distribución Beta surge precisamente para resolver este problema.

Supongamos que queremos estimar la probabilidad:

$$
\theta = P(\text{éxito})
$$

Por ejemplo:

* Probabilidad de que una moneda produzca cara.
* Probabilidad de que un pasajero sobreviva.
* Probabilidad de que un estudiante apruebe un examen.
* Probabilidad de que un cliente realice una compra.

Inicialmente desconocemos el valor de (\theta). No sabemos si vale:

$$
0.2,\quad 0.5,\quad 0.8
$$

o cualquier otro valor entre 0 y 1.

La distribución Beta permite describir qué tan plausibles consideramos los distintos valores de dicha probabilidad.

---

### Distribución Beta

La distribución Beta depende de dos parámetros: $\alpha$ y $\beta$

y posee función de densidad:

$$
f(\theta)=
\frac{\theta^{\alpha-1}(1-\theta)^{\beta-1}}
{B(\alpha,\beta)}
$$

para:

$$
0 \le \theta \le 1
$$

donde:

$$
B(\alpha,\beta)
$$

es una constante de normalización.

---

### Interpretación de los parámetros

Intuitivamente:

* $\alpha$ representa evidencia acumulada a favor del éxito.
* $\beta$ representa evidencia acumulada a favor del fracaso.

Por esta razón, al observar:

* $n_E$ éxitos,
* $n_F$ fracasos,

la distribución posterior toma la forma:

$$
Beta(n_E+1,n_F+1)
$$

---

### Ejemplo

Supongamos que lanzamos una moneda y observamos:

* 3 caras.
* 1 sello.

La distribución posterior será:

$$
Beta(4,2)
$$

La mayor parte de la probabilidad se concentra alrededor de valores cercanos a:

$$
\theta \approx 0.67
$$

pero todavía existe incertidumbre.

---

### El papel de la evidencia

Ahora comparemos dos situaciones:

#### Caso 1

* 3 caras.
* 1 sello.

$$
Beta(4,2)
$$

#### Caso 2

* 300 caras.
* 100 sellos.

$$
Beta(301,101)
$$

En ambos casos la proporción observada es aproximadamente:
$$
0.75
$$

Sin embargo, la segunda distribución es mucho más estrecha.

Esto significa que nuestra incertidumbre es considerablemente menor.

---

### Aprender como reducción de incertidumbre

La media de la distribución Beta nos indica cuál es el valor más probable del parámetro.

La dispersión de la distribución nos indica qué tan seguros estamos de dicha estimación.

Por esta razón, el aprendizaje puede interpretarse como un proceso de reducción progresiva de incertidumbre.

A medida que aumenta el número de observaciones:

* La distribución posterior se concentra.
* La varianza disminuye.
* La incertidumbre disminuye.

Es importante notar que la incertidumbre que disminuye no es la incertidumbre del fenómeno observado, sino la incertidumbre que tenemos acerca de sus parámetros.


---

## Likelihood y Maximum Likelihood

En la unidad anterior aprendimos a construir distribuciones empíricas a partir de datos observados y a compararlas con modelos teóricos mediante medidas como la divergencia KL y pruebas de bondad de ajuste.

Ahora surge una nueva pregunta:

> Si conocemos la forma de una distribución, ¿cómo encontramos los valores de sus parámetros?

La respuesta se encuentra en el concepto de verosimilitud o likelihood.

---

### El problema

Supongamos que observamos los siguientes datos:

$$
x_1,x_2,\ldots,x_n
$$

y creemos que provienen de una distribución:

$$
q(x;\theta)
$$

donde:

$$
\theta
$$

representa parámetros desconocidos.

Por ejemplo:

* En una Bernoulli, $\theta=p$.
* En una Poisson, $\theta=\lambda$.
* En una Normal, $\theta=(\mu,\sigma)$.

Nuestro objetivo es estimar dichos parámetros.

---

### Likelihood

La likelihood responde a la siguiente pregunta:

> Si los parámetros fueran $\theta$, ¿qué tan probable sería observar los datos obtenidos?

La función de verosimilitud se define como:

$$
L(\theta)
=
P(x_1,x_2,\ldots,x_n|\theta)
$$

Si suponemos observaciones independientes:

$$
L(\theta)
=
\prod_{i=1}^{n}
q(x_i;\theta)
$$

---

### Interpretación

Es importante destacar que la likelihood no es una distribución de probabilidad sobre $\theta$.

Los datos ya fueron observados.

La likelihood mide qué tan compatibles son los datos con distintos valores posibles de los parámetros.

---

### Ejemplo: moneda

Supongamos que observamos:

* 8 caras.
* 2 sellos.

Si proponemos:

$$
\theta=P(\text{cara})
$$

la likelihood será:

$$
L(\theta)
=

\theta^8(1-\theta)^2
$$

Algunos valores de $\theta$ explicarán mejor los datos que otros.

Por ejemplo:

* $\theta=0.8$ produce una likelihood alta.
* $\theta=0.2$ produce una likelihood muy baja.

---

### Maximum Likelihood Estimation (MLE)

La estimación por máxima verosimilitud consiste en encontrar el valor de los parámetros que maximiza la likelihood:

$$
\theta^*
=

\arg\max_{\theta}
L(\theta)
$$

En palabras:

> Elegimos los parámetros que hacen que los datos observados sean lo más probables posible.

---

### Log-Likelihood

Debido a que la likelihood suele involucrar productos muy grandes, normalmente se utiliza su logaritmo:

$$
\ell(\theta)
=

\log L(\theta)
$$

Utilizando propiedades de los logaritmos:

$$
\ell(\theta)
=

\sum_i
\log q(x_i;\theta)
$$

Esto simplifica considerablemente los cálculos.

---

### Ejemplo: Maximum Likelihood para una moneda

Supongamos que lanzamos una moneda 10 veces y observamos:

* 8 caras.
* 2 sellos.

Deseamos estimar:

$$
\theta=P(\text{cara})
$$

---

### Función de Likelihood

Cada lanzamiento puede modelarse mediante una distribución Bernoulli:

$$
X_i \sim Bernoulli(\theta)
$$

Como los lanzamientos son independientes:

$$
L(\theta)
=

\prod_{i=1}^{10}
P(x_i|\theta)
$$

En nuestro experimento observamos:

* 8 éxitos (caras),
* 2 fracasos (sellos).

Por lo tanto:

$$
L(\theta)
=

\theta^8(1-\theta)^2
$$

Esta función indica qué tan compatibles son distintos valores de (\theta) con los datos observados.

Por ejemplo:

* $($\theta=0.8$)$ produce una likelihood alta.
* $\theta=0.2$ produce una likelihood muy baja.

---

### Log-Likelihood

Para facilitar los cálculos tomamos logaritmos:

$$
\ell(\theta)
=

\log L(\theta)
$$

Entonces:

$$
\ell(\theta)
=

\log\left(
\theta^8(1-\theta)^2
\right)
$$

Aplicando propiedades de los logaritmos:

$$
\ell(\theta)
=

8\log(\theta)
+
2\log(1-\theta)
$$

Esta función posee exactamente el mismo máximo que la likelihood original.

---

### Maximización

Para encontrar el valor óptimo derivamos respecto a (\theta):

$$
\frac{d\ell}{d\theta}
=

 \frac{8}{\theta}
-
\frac{2}{1-\theta}
$$

Buscamos los puntos críticos:

$$
\frac{8}{\theta}
-
 \frac{2}{1-\theta}
=
0
$$

Lo que lleva a la solución: 

$$
\theta^*
=\frac{8}{10}
=
0.8
$$

### Resultado

La estimación de máxima verosimilitud es:

$$
\hat\theta_{MLE}
=
0.8
$$

Es decir:

$$
P(\text{cara})
=

0.8
$$
---

### Relación con la inferencia bayesiana

Es importante notar una diferencia fundamental entre Maximum Likelihood e Inferencia Bayesiana.

Maximum Likelihood produce un único valor:

[
\theta=0.8
]

La inferencia bayesiana produce una distribución completa sobre los posibles valores de (\theta):

[
\theta
\sim
Beta(9,3)
]

Ambos enfoques utilizan los mismos datos, pero responden preguntas diferentes.

```text
Maximum Likelihood:
¿Cuál es el valor más probable de θ?

Bayes:
¿Cuál es la distribución de probabilidad completa de θ?
```

En las siguientes secciones veremos que ambos enfoques están profundamente relacionados y que, cuando el número de observaciones aumenta, sus resultados tienden a converger.


---
### Relación con la divergencia KL

Existe una conexión profunda entre Maximum Likelihood y la teoría de la información.

Cuando el tamaño de muestra es suficientemente grande, maximizar la likelihood equivale a minimizar la divergencia KL entre:

$$
\hat p(x)
$$

y

$$
q(x;\theta)
$$

Es decir, los parámetros obtenidos por MLE son aquellos que producen la menor distancia informacional entre el modelo y los datos observados.

---

### Interpretación moderna

La mayor parte del aprendizaje estadístico y del aprendizaje automático puede entenderse como una extensión de esta idea.

El proceso general es:

```text
Datos observados
        ↓
Modelo paramétrico
        ↓
Likelihood
        ↓
Estimación de parámetros
        ↓
Mejor ajuste posible
```

Desde esta perspectiva, aprender consiste en encontrar los parámetros que mejor explican la evidencia disponible.

