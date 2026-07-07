# Unidad 1 — Datos, incertidumbre y representación empírica

## Pandas y manipulación de datos, Limpieza y transformación de datasets

Vamos a mirar un conjunto de libros para repasar conceptos de pandas, de carga de datos y de manipulación de los mismos. 

### Operaciones con DataFrames y Pandas:  
- Introduccion a la librería pandas: [Libro 1](./libro1.ipynb)
- Operaciones de filtrado: [Libro 2](./libro2.ipynb)
- Operaciones de Mapeo: - [Libro 3](./libro3.ipynb)
- Operaciones de Mapeo, funciones lambda: [Libro 4](./libro4.ipynb)
- Operaciones de reducción: [Libro 5](./libro5.ipynb)
- Combinación de las operaciones de filtrado, mapeo y reducción: [Libro 6](./libro6.ipynb)
### Operaciones de resumen y combinación de dataframes
- Operación groupBy: [Libro 6](./libro7.ipynb)
- Operación Merge entre DataFrames: [Libro 8](./libro8.ipynb)
- Operación Join entre DataFrames: [Libro 9](./libro9.ipynb)
- Tablas dinámicas en Pandas: [Libro 10](./libro10.ipynb) 
### Visualización de información
- Visualización con PyPlot: [Libro 11](./libro11.ipynb)
- Visualización con Seaborn: [Libro 12](./libro12.ipynb) 
- Visualización con Plotly: [Libro 13](./libro13.ipynb)

## Estadística descriptiva univariable y multivariable
### Estadística descriptiva univariable:  
**Qué elementos debe contener?**  Las principales medidas de estadística descriptiva son técnicas utilizadas para resumir y describir las características principales de un conjunto de datos. Algunas de las medidas más importantes son: 
- Medidas de Tendencia Central: 
    - Media: El promedio aritmético de un conjunto de valores. 
    - Mediana: El valor medio de un conjunto de datos cuando estos están ordenados. 
    - Moda: El valor que ocurre con mayor frecuencia en un conjunto de datos. 
- Medidas de Dispersión: 
    - Rango: La diferencia entre el valor máximo y mínimo en un conjunto de datos. 
    - Varianza: Una medida de cuán dispersos están los valores en un conjunto de datos. 
    - Desviación Estándar: La raíz cuadrada de la varianza, proporcionando una medida más interpretable de la dispersión. 
- Medidas de Forma: 
    - Asimetría (Skewness): Una medida de la asimetría de una distribución. La asimetría positiva indica una cola derecha más larga, mientras que la asimetría negativa indica una cola izquierda más larga. 
    - Curtosis (Kurtosis): Una medida de la "colas" de una distribución. Evalúa si los datos tienen colas pesadas o ligeras en comparación con una distribución normal. 
- Percentiles y Cuartiles: 
    - Percentiles: Valores que dividen un conjunto de datos en 100 partes iguales. Por ejemplo, el percentil 25 es el valor por debajo del cual se encuentra el 25% de los datos. 
    - Cuartiles: Valores que dividen un conjunto de datos en cuatro partes iguales. El primer cuartil (Q1) es el percentil 25, el segundo cuartil (Q2) es la mediana, y el tercer cuartil (Q3) es el percentil 75. 
Estas medidas de estadística descriptiva proporcionan un resumen conciso de las principales características de un conjunto de datos, ayudando a comprender su distribución, tendencia central y variabilidad. Son fundamentales para explorar y resumir datos antes de realizar análisis más avanzados. 

### Estadística descriptiva multivariable

La estadística descriptiva tradicional se enfoca en estudiar una variable a la vez, analizando su distribución, tendencia central, dispersión y forma. Sin embargo, en la mayoría de los problemas reales existen múltiples variables que interactúan entre sí. La estadística descriptiva multivariable busca comprender estas relaciones antes de construir modelos predictivos o explicativos.

#### Relación entre variables

Una de las primeras preguntas que surgen al analizar un conjunto de datos es si el comportamiento de una variable depende de otra. Por ejemplo:

- ¿Las horas de sueño afectan el nivel de concentración?
- ¿El consumo de café se relaciona con el estrés?
- ¿La satisfacción de un estudiante depende del programa académico al que pertenece?

Para responder estas preguntas se utilizan diferentes herramientas descriptivas.

#### Estadísticos condicionados por grupos

Es posible calcular estadísticas descriptivas para subconjuntos de datos definidos por una variable categórica.

Por ejemplo:

- Media de horas de sueño por semestre.
- Varianza del promedio académico por programa.
- Distribución del estrés según género.
- Nivel de satisfacción según modalidad de estudio.

Este tipo de análisis permite identificar diferencias entre grupos y posibles patrones de comportamiento.

#### Tablas cruzadas y distribuciones conjuntas

Cuando se estudian dos variables categóricas se utilizan tablas de contingencia o tablas cruzadas para analizar la frecuencia con que ocurren determinadas combinaciones.

Por ejemplo:

| Estrés | Bajo | Medio | Alto |
|----------|----------|----------|----------|
| Dormir más de 7h | 40 | 25 | 5 |
| Dormir menos de 7h | 10 | 35 | 45 |

Estas tablas permiten estimar probabilidades conjuntas y probabilidades condicionadas, fundamentales para el análisis bayesiano y la teoría de la información.

#### Covarianza

La covarianza mide cómo varían conjuntamente dos variables.

- Covarianza positiva: ambas variables tienden a aumentar o disminuir juntas.
- Covarianza negativa: cuando una aumenta, la otra tiende a disminuir.
- Covarianza cercana a cero: no existe una relación lineal evidente.

Aunque su magnitud depende de las unidades de medida, proporciona una primera aproximación a la dependencia entre variables.

#### Correlación

La correlación normaliza la covarianza y permite medir la intensidad de la relación lineal entre dos variables.

Sus valores se encuentran entre:

- -1: relación lineal negativa perfecta.
- 0: ausencia de relación lineal.
- 1: relación lineal positiva perfecta.

La correlación permite comparar relaciones entre variables con diferentes escalas de medición.

#### Matriz de correlación

Cuando existen múltiples variables resulta útil construir una matriz de correlación que muestre simultáneamente las relaciones entre todas las variables del conjunto de datos.

Esta matriz permite:

- Identificar variables redundantes.
- Detectar grupos de variables relacionadas.
- Descubrir posibles factores latentes.
- Preparar los datos para técnicas de reducción de dimensionalidad.

#### Información mutua

La correlación mide únicamente relaciones lineales. Sin embargo, dos variables pueden estar relacionadas de forma no lineal.

La información mutua mide cuánto disminuye la incertidumbre sobre una variable cuando se conoce otra. Desde la teoría de la información, puede interpretarse como la cantidad de información compartida entre dos variables.

Este concepto será fundamental para comprender árboles de decisión, inferencia bayesiana, procesamiento de lenguaje natural y modelos modernos de inteligencia artificial.

#### Visualización multivariable

Las relaciones entre variables pueden explorarse mediante:

- Diagramas de dispersión.
- Pairplots.
- Mapas de calor de correlación.
- Diagramas de cajas por grupos.
- Gráficos tridimensionales.
- Visualizaciones de componentes principales.

La visualización permite identificar patrones que no son evidentes únicamente mediante estadísticas numéricas.

#### Objetivo de la estadística descriptiva multivariable

El propósito final no es únicamente resumir datos, sino comprender la estructura de relaciones existente entre las variables observadas. Este conocimiento permitirá posteriormente construir modelos probabilísticos, reducir incertidumbre, identificar variables informativas y desarrollar representaciones más compactas de la información mediante técnicas como PCA y análisis factorial.

Puede ver un ejemplo en este libro:  [Estadística descriptiva](./estadistica_descriptiva.ipynb). El límite del análisis es todo lo que usted pueda encontrar y pueda describir como relación entre variables.  

## Distribuciones de probabilidad empíricas, obteniendo probabilidades desde frecuencias

### Introducción

La mayoría de los modelos probabilísticos parten de una distribución de probabilidad desconocida que representa el comportamiento de un fenómeno real. Sin embargo, en la práctica rara vez conocemos dicha distribución. Lo que normalmente observamos es una colección finita de datos obtenidos mediante mediciones, encuestas, experimentos o registros históricos.

Esta colección de observaciones constituye una **muestra**.

El objetivo inicial de la estadística consiste en utilizar esta muestra para construir una aproximación de la distribución de probabilidad que generó los datos.

---

### Población y muestra

Supongamos que existe una variable aleatoria: $$ X \sim p(x) $$

donde $p(x)$ representa la distribución real del fenómeno.

Por ejemplo:

* Número de cafés consumidos por un estudiante durante un día.
* Cantidad de visitas diarias a una página web.
* Horas de sueño de una persona.
* Tiempo de permanencia en una biblioteca.

La distribución $p(x)$ es generalmente desconocida.

Lo que observamos son muestras:

$$ x_1, x_2, ..., x_n $$

obtenidas de dicha distribución.

La pregunta fundamental es:

> ¿Cómo podemos aproximar (p(x)) utilizando únicamente las observaciones disponibles?

---

### Distribución empírica

La forma más sencilla de construir una distribución consiste en calcular frecuencias observadas.

Supongamos el siguiente conjunto de observaciones, que representan el número de personas que toman al día cierto número de porciones de café:

| Número de cafés | Frecuencia |
| --------------- | ---------- |
| 0               | 5          |
| 1               | 10         |
| 2               | 20         |
| 3               | 12         |
| 4               | 3          |

La muestra contiene:

$$
N = 50
$$

observaciones.

La probabilidad empírica se calcula como:

$$ \hat p(x)=\frac{n_x}{N} $$

donde:

* $n_x$ es el número de veces que aparece el valor (x).
* $N$ es el número total de observaciones.

Por ejemplo:

$$
\hat p(2)=\frac{20}{50}=0.4
$$

Esta distribución construida a partir de frecuencias observadas recibe el nombre de **distribución empírica**.

---

### Interpretación

La distribución empírica representa nuestro mejor conocimiento del fenómeno utilizando únicamente los datos disponibles.

A medida que aumenta el número de observaciones:

$$
\hat p(x)
\rightarrow
p(x)
$$

según la Ley de los Grandes Números.

Esto significa que una muestra más grande generalmente produce una representación más estable y precisa de la realidad.

---

### Variables discretas

Las distribuciones empíricas son particularmente sencillas cuando la variable toma un número finito o contable de valores.

Ejemplos:

* Número de hermanos.
* Número de cafés diarios.
* Número de visitas a una página web.
* Número de veces que se utiliza un espacio durante un día.

En estos casos basta con contar frecuencias y normalizarlas para obtener probabilidades.

Las distribuciones discretas permiten introducir naturalmente conceptos como (que estudiaremos luego):

* Probabilidad.
* Entropía.
* Información mutua.
* Probabilidad condicional.
* Inferencia bayesiana.

---

### Variables continuas

Las variables continuas presentan un desafío adicional.

Ejemplos:

* Horas de sueño.
* Edad.
* Temperatura.
* Tiempo de permanencia.
* Distancia recorrida.

En una variable continua es improbable que dos observaciones tengan exactamente el mismo valor.

Por ejemplo:

```text
6.31 horas
6.28 horas
6.44 horas
6.37 horas
```

Cada observación puede ser distinta.

Si intentáramos construir una distribución empírica utilizando frecuencias exactas, prácticamente todos los valores tendrían frecuencia uno.

---

### Histogramas y discretización

Para representar variables continuas se agrupan observaciones en intervalos.

Por ejemplo:

| Horas de sueño | Frecuencia |
| -------------- | ---------- |
| 4-5 h          | 12         |
| 5-6 h          | 35         |
| 6-7 h          | 54         |
| 7-8 h          | 28         |
| 8-9 h          | 11         |

Estos intervalos reciben el nombre de **bins**.

El histograma puede interpretarse como una aproximación discreta de una distribución continua.

---

### El problema de la resolución

En variables continuas la distribución empírica depende de cómo se construyan los intervalos.

Pocos intervalos:

* Pierden detalle.
* Suavizan la distribución.

Muchos intervalos:

* Introducen ruido.
* Hacen visible la variabilidad muestral.

Este problema motiva posteriormente el uso de distribuciones paramétricas como:

* Normal.
* Exponencial.
* Poisson.
* Gamma.
* Weibull.

### Trabajo en clase: 

Vamos a analizar el dataset de los pasajeros del Titanic, para mirar las diferentes distribuciones de probabilidad muestrales que podemos obtener. Mirar este libro [Libro Titanic](./distribuciones_empiricas.ipynb)

### Reflexión

La distribución empírica constituye el primer paso en la construcción de modelos probabilísticos.

Antes de asumir que los datos siguen una distribución Normal, Poisson o Exponencial, debemos comprender qué nos dicen realmente las observaciones.

La estadística moderna puede interpretarse como un proceso de transición desde:

```text
Datos observados
        ↓
Frecuencias observadas
        ↓
Distribución empírica
        ↓
Modelo probabilístico
        ↓
Inferencia y predicción
```

Toda la teoría posterior del curso se apoyará sobre esta idea fundamental: utilizar muestras para construir representaciones probabilísticas de una realidad parcialmente observada.

## Variables aleatorias y distribuciones de probabilidad

### Introducción

Una vez que disponemos de una muestra y hemos construido una distribución empírica, surge una pregunta fundamental:

> ¿Existe una función matemática capaz de representar el comportamiento observado en los datos?

Las distribuciones de probabilidad son modelos matemáticos diseñados para describir cómo se generan los valores de una variable aleatoria.

Una **variable aleatoria** es una variable cuyo valor depende del resultado de un fenómeno incierto.

Ejemplos:

* Número de clientes que llegan a una cafetería durante una hora.
* Cantidad de veces que una persona utiliza un espacio durante un día.
* Edad de los pasajeros de un barco.
* Tiempo de espera para recibir un mensaje.
* Resultado de lanzar un dado.

Las variables aleatorias pueden ser:

### Variables discretas

Toman valores aislados y contables.

Ejemplos:

* Número de hijos.
* Número de visitas.
* Resultado de un dado.

### Variables continuas

Pueden tomar cualquier valor dentro de un intervalo.

Ejemplos:

* Tiempo.
* Peso.
* Temperatura.
* Edad.

---

### Distribución Bernoulli

#### ¿Qué representa?

Describe experimentos con únicamente dos posibles resultados.

Ejemplos:

* Éxito o fracaso.
* Sobrevive o no sobrevive.
* Compra o no compra.
* Aprueba o reprueba.

#### Parámetro

$$
p=P(X=1)
$$

donde $p$ representa la probabilidad de éxito.

#### Función de probabilidad

$$
P(X=x)=p^x(1-p)^{1-x}
$$

para:

$$
x\in{0,1}
$$

Lo cual también se puede ver en la tabla: 
| x | P(X=x) |
| - | ------ |
| 0 | $1-p$  |
| 1 | $p$    |

---

### Distribución Binomial

#### ¿Qué representa?

Describe el número de éxitos obtenidos al repetir un experimento Bernoulli varias veces. El punto crítico es que cada experimento es independiente estadísticamente de los otros experimentos. 

#### Ejemplos

* Número de estudiantes que aprueban un examen.
* Número de clientes que realizan una compra.
* Número de caras al lanzar una moneda.

#### Parámetros

- $n$ Número de ensayos.
- $p$ Probabilidad de éxito.

#### Función de probabilidad

$$
P(X=k)=
\binom{n}{k}
p^k
(1-p)^{n-k}
$$

---

### Distribución Poisson

#### ¿Qué representa?

Modela conteos de eventos que ocurren aleatoriamente en un intervalo de tiempo o espacio, cuando existe una tasa o velocidad de ocurrencia de los eventos por intervalo de tiempo o de espacio. 

#### Ejemplos

* Clientes que llegan a una tienda por hora.
* Correos electrónicos recibidos por día.
* Uso de un baño durante una jornada.
* Accidentes por semana.

#### Parámetro

$\lambda$ Número esperado de eventos, tasa o velocidad de ocurrencia.

#### Función de probabilidad

$$
P(X=k)=
\frac{\lambda^k e^{-\lambda}}{k!}
$$

---

### Distribución Uniforme Discreta

#### ¿Qué representa?

Describe una situación en la que todos los resultados posibles tienen exactamente la misma probabilidad de ocurrir.

Es una de las distribuciones más simples y constituye un modelo natural cuando no existe información que favorezca un resultado sobre otro.

#### Ejemplos

- Lanzamiento de un dado equilibrado.
- Extracción aleatoria de una carta de una baraja.
- Selección aleatoria de un estudiante de un grupo.
- Selección aleatoria de una palabra dentro de un diccionario.

#### Parámetros

La distribución depende únicamente del número de resultados posibles:

$
n
$

#### Función de probabilidad

Si existen $n$ resultados posibles:

$$
P(X=x)=\frac{1}{n}
$$

para:

$$
x \in \{x_1,x_2,\dots,x_n\}
$$

#### Ejemplo: lanzamiento de un dado

$$
X \in \{1,2,3,4,5,6\}
$$

y

$$
P(X=x)=\frac{1}{6}
$$

para cada una de las caras.

| Resultado | Probabilidad |
|------------|-------------|
| 1 | 1/6 |
| 2 | 1/6 |
| 3 | 1/6 |
| 4 | 1/6 |
| 5 | 1/6 |
| 6 | 1/6 |


--- 


### Distribución Uniforme continua

#### ¿Qué representa?

Todos los valores dentro de un intervalo son igualmente probables.

#### Ejemplos

* Posición aleatoria sobre una recta.
* Número aleatorio generado por computador.
* Experimento de Bayes de la moneda sobre la mesa.

#### Parámetros

[
a,b
]

Límites inferior y superior.

#### Función de densidad

$$
f(x)=\frac{1}{b-a}
$$

para:

$ a\le x \le b $

---

### Distribución Exponencial

#### ¿Qué representa?

Modela tiempos de espera entre eventos consecutivos de un proceso Poisson.

#### Ejemplos

* Tiempo hasta la llegada del próximo cliente.
* Tiempo hasta una llamada telefónica.
* Tiempo hasta una falla.

#### Parámetro

$\lambda$ Tasa de ocurrencia.

#### Función de densidad
$$
f(x)=
\lambda e^{-\lambda x}
$$

para:

$$
x\ge 0
$$

---

### Distribución Normal (Gaussiana)

#### ¿Qué representa?

Es una de las distribuciones más importantes de la estadística.

Aparece cuando una variable es el resultado de muchos factores pequeños independientes.

#### Ejemplos

* Estaturas.
* Errores de medición.
* Calificaciones.
* Variables biológicas.

#### Parámetros

Media: $\mu$

Desviación estándar: $\sigma$

#### Función de densidad

$$
f(x)=
\frac{1}{\sqrt{2\pi\sigma^2}}
e^{-\frac{(x-\mu)^2}{2\sigma^2}}
$$

---

### Distribución Beta

#### ¿Qué representa?

La distribución Beta no describe directamente una variable observable como la edad, el número de clientes o el tiempo de espera.

La distribución Beta describe nuestra incertidumbre acerca de una **probabilidad desconocida**.

Supongamos que queremos estimar:

$$
\theta=P(\text{éxito})
$$

Por ejemplo:

- Probabilidad de que un estudiante apruebe un examen.
- Probabilidad de que una persona compre un producto.
- Probabilidad de que un paciente responda a un tratamiento.
- Probabilidad de que un pasajero sobreviva al Titanic.

Inicialmente no conocemos el valor de $\theta$.

La distribución Beta permite representar qué tan plausibles consideramos distintos valores de dicha probabilidad.

---

#### Intuición

Mientras que una distribución Normal podría responder:

> ¿Qué valores puede tomar una variable?

La distribución Beta responde:

> ¿Qué valores puede tomar una probabilidad desconocida?

Por esta razón su dominio está restringido al intervalo:

$$
0 \le \theta \le 1
$$

---

#### Ejemplo intuitivo

Supongamos que una moneda es desconocida.

No sabemos si:

$$
\theta=P(\text{cara})
$$

vale:

- 0.5
- 0.6
- 0.8
- 0.3

o cualquier otro valor entre 0 y 1.

Antes de observar lanzamientos podríamos considerar todos los valores igualmente plausibles.

En este caso:

$$
\theta \sim Beta(1,1)
$$

que corresponde a una distribución uniforme.

---

#### Aprendizaje mediante evidencia

Ahora observamos:

- 8 caras
- 2 sellos

La evidencia sugiere que $\theta$ probablemente es mayor que 0.5.

La distribución posterior se concentra alrededor de valores cercanos a:

$$
\theta \approx 0.8
$$

La Beta permite describir esta actualización de conocimiento.

#### Parámetros

$$
\alpha,\beta
$$

que representan evidencia acumulada.

#### Función de densidad

$$
f(x)=
\frac{x^{\alpha-1}(1-x)^{\beta-1}}
{B(\alpha,\beta)}
$$

---

### Distribuciones empíricas versus distribuciones paramétricas

Hasta ahora hemos estudiado dos formas de representar incertidumbre:

#### Distribución empírica

Se construye directamente desde las observaciones.

$$
\hat p(x)=\frac{n_x}{N}
$$

#### Distribución paramétrica

Se asume una familia matemática y se estiman sus parámetros.

$$
q(x;\theta)
$$

Por ejemplo:

* Bernoulli: $p$
* Binomial: $n,p$
* Poisson: $\lambda$
* Normal: $\mu,\sigma$

El resto del curso estará dedicado a estudiar cómo seleccionar y ajustar estos modelos a partir de los datos observados.

---

## De distribuciones empíricas a modelos probabilísticos

### Introducción

Una vez construida una distribución empírica a partir de una muestra, surge una pregunta fundamental:

> ¿Existe una distribución teórica capaz de describir el comportamiento observado en los datos?

Por ejemplo:

* ¿Las edades de los pasajeros del Titanic siguen una distribución Normal?
* ¿La cantidad de visitas diarias a un sitio web sigue una distribución Poisson?
* ¿Los tiempos de espera entre clientes siguen una distribución Exponencial?

Responder estas preguntas permite reemplazar una tabla de frecuencias por un modelo matemático más compacto y generalizable.

---

### Distribuciones empíricas y distribuciones paramétricas

Hasta ahora hemos construido una distribución empírica:

$$
\hat p(x)
$$

directamente a partir de los datos observados.

Sin embargo, muchas distribuciones teóricas pueden describirse mediante una pequeña cantidad de parámetros.

Por ejemplo:

| Distribución | Parámetros     |
| ------------ | -------------- |
| Bernoulli    | $p$            |
| Binomial     | $n,p$          |
| Poisson      | $\lambda$      |
| Exponencial  | $\lambda$      |
| Normal       | $\mu,\sigma$   |
| Beta         | $\alpha,\beta$ |

Una distribución paramétrica puede escribirse como:

$$
q(x;\theta)
$$

donde: $\theta$ representa el conjunto de parámetros desconocidos.

---

### El problema de ajuste

Disponemos de:

$$
\hat p(x)
$$

obtenida desde los datos.

Y proponemos un modelo:

$$
q(x;\theta)
$$

Nuestro objetivo consiste en encontrar los valores de $ \theta $ que produzcan el mejor ajuste posible entre ambas distribuciones.

---

### Ejemplo: distribución Normal

Supongamos que observamos las edades de los pasajeros del Titanic.

Podemos proponer que:

$$
X \sim \mathcal N(\mu,\sigma)
$$

Sin embargo:

* no conocemos $\mu$,
* no conocemos $\sigma$.

Los datos deben permitirnos estimarlos.

Una estimación natural consiste en utilizar:

$$
\hat\mu = \text{media muestral}
$$

y

$$
\hat\sigma = \text{desviación estándar muestral}
$$

obteniendo una distribución Normal ajustada a los datos observados.

---

### ¿Cómo sabemos si el ajuste es bueno?

Una vez estimados los parámetros surge una nueva pregunta:

> ¿Qué tan parecida es la distribución teórica a la distribución empírica observada?

Existen diferentes herramientas para responder esta pregunta.

---

#### Distancia de Kullback-Leibler (KL)

La distancia de Kullback-Leibler mide cuánta información se pierde cuando una distribución es utilizada para aproximar otra.

Si:

$$
\hat p(x)
$$

es la distribución empírica observada y

$$
q(x;\theta)
$$

es el modelo propuesto, la divergencia KL se define como:

$$
D_{KL}(\hat p \parallel q)=
\sum_x
\hat p(x)
\log
\frac{\hat p(x)}
{q(x;\theta)}
$$

para variables discretas.

---

#### Interpretación

* KL = 0 → ambas distribuciones son idénticas.
* KL pequeña → el modelo describe bien los datos.
* KL grande → el modelo describe mal los datos.

La divergencia KL no es una distancia en sentido matemático estricto, pero constituye una medida muy importante en estadística, teoría de la información e inteligencia artificial.

---

#### Interpretación conceptual

La divergencia KL responde a la pregunta:

> ¿Cuánta información adicional necesito porque estoy utilizando el modelo equivocado?

Por esta razón se convertirá posteriormente en una de las herramientas fundamentales para comprender:

* Maximum Likelihood.
* Cross Entropy.
* Aprendizaje estadístico.
* Redes neuronales.
* Modelos de lenguaje.

---

#### Prueba Chi-Cuadrado de Bondad de Ajuste

Su objetivo es determinar si las diferencias observadas entre los datos y una distribución teórica pueden atribuirse al azar.

---

Hipótesis nula:

$
H_0:
\text{Los datos provienen de la distribución propuesta}
$

Hipótesis alternativa:

$
H_1:
\text{Los datos no provienen de la distribución propuesta}
$

---

#### Estadístico

$$
\chi^2
=
\sum_i
\frac{(O_i-E_i)^2}
{E_i}
$$

donde:

* $O_i$: frecuencia observada.
* $E_i$: frecuencia esperada según el modelo.

---

#### Interpretación

Valores pequeños de:

$$
\chi^2
$$

indican que las diferencias observadas son compatibles con el azar.

Valores grandes sugieren que la distribución propuesta no describe adecuadamente los datos.

---

#### Aplicaciones

Especialmente útil para:

* Distribuciones discretas.
* Datos agrupados.
* Tablas de frecuencias.

---

#### Prueba de Kolmogorov-Smirnov

Su objetivo es comparar una distribución empírica con una distribución teórica sin necesidad de agrupar los datos.

---

#### Idea principal

En lugar de comparar frecuencias, compara las funciones de distribución acumulada.

Sea:

$$
F_n(x)
$$

la distribución acumulada empírica.

$$F(x)$$

la distribución acumulada teórica.

La prueba utiliza:

$$
D
=
\sup_x
|F_n(x)-F(x)|
$$

---

#### Interpretación

* $D$ pequeño → las distribuciones son similares.
* $D$ grande → las distribuciones difieren significativamente.

---

#### Aplicaciones

Particularmente útil para:

* Variables continuas.
* Normalidad.
* Exponencial.
* Uniforme.
* Comparaciones no agrupadas.

---

# Comparación de las herramientas

| Método             | ¿Qué mide?                                          | Tipo de variable        |
| ------------------ | --------------------------------------------------- | ----------------------- |
| KL                 | Distancia informacional                             | Discreta o continua     |
| Chi-Cuadrado       | Diferencia entre frecuencias observadas y esperadas | Principalmente discreta |
| Kolmogorov-Smirnov | Diferencia entre distribuciones acumuladas          | Principalmente continua |

---

#### Reflexión

Hasta ahora hemos seguido el siguiente camino:

```text
Datos observados
        ↓
Distribución empírica
        ↓
Distribución teórica candidata
        ↓
Estimación de parámetros
        ↓
Comparación entre modelos y datos
```

A partir de este momento surge una nueva pregunta:

> Si los parámetros de una distribución son desconocidos, ¿cómo podemos estimarlos de manera sistemática utilizando únicamente los datos observados?

La respuesta a esta pregunta nos llevará a la inferencia estadística, la estimación por máxima verosimilitud y la inferencia bayesiana, temas que estudiaremos en las siguientes unidades.

Lo que más me gusta de esta narrativa es que la entropía y la KL ya no aparecen como conceptos aislados. Aparecen porque el estudiante tiene una necesidad concreta: **comparar una distribución empírica obtenida de los datos con un modelo teórico propuesto**. Ahí la KL se vuelve una herramienta natural y Bayes queda preparado para la siguiente unidad.
