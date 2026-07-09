# Unidad 3 — Modelado estadístico, información y generalización

# Introducción

## Una pregunta aparentemente sencilla

Hasta ahora hemos aprendido a construir distribuciones de probabilidad a partir de datos, a estimar parámetros mediante Maximum Likelihood y a actualizar nuestras creencias utilizando el Teorema de Bayes.

En todos esos casos aparecía una misma idea de fondo:

> A partir de un conjunto de observaciones somos capaces de aprender algo acerca del mundo.

Pero esta afirmación plantea inmediatamente una nueva pregunta.

**¿Qué significa realmente aprender?**

Cuando decimos que un algoritmo "aprendió", ¿qué fue exactamente lo que aprendió? ¿Memorizó los datos? ¿Descubrió las ecuaciones que gobiernan el fenómeno? ¿Encontró relaciones ocultas? ¿O simplemente construyó una aproximación suficientemente buena de la realidad?

Responder estas preguntas constituye uno de los objetivos principales del aprendizaje estadístico y del aprendizaje automático.

---

## El mundo es demasiado complejo

Imaginemos que deseamos construir un sistema capaz de predecir la temperatura del día siguiente. Podríamos pensar que basta con observar las temperaturas de los últimos días y buscar algún patrón. Sin embargo, rápidamente descubrimos que la temperatura depende de una enorme cantidad de factores:

* presión atmosférica,
* humedad,
* velocidad del viento,
* nubosidad,
* corrientes oceánicas,
* radiación solar,
* relieve,
* vegetación,
* estaciones del año,
* e incluso fenómenos ocurridos a cientos o miles de kilómetros de distancia.

La realidad posee una complejidad extraordinaria. Modelarla exactamente resulta prácticamente imposible. Esta situación no ocurre únicamente en meteorología. Sucede prácticamente en cualquier disciplina. 

Por ejemplo:

* El comportamiento de un paciente depende de cientos de variables fisiológicas.

* El precio de una acción depende de miles de decisiones humanas.

* El movimiento de una persona dentro de una vivienda depende de innumerables factores físicos, psicológicos y sociales.

Incluso sistemas aparentemente sencillos esconden una enorme complejidad.

---

## No aprendemos la realidad

Una consecuencia importante de esta observación es la siguiente:

> Ningún algoritmo aprende la realidad tal como es.

Lo que realmente aprende es una representación simplificada de ella. Dicha representación recibe el nombre de **modelo**. Un modelo intenta conservar únicamente aquellos aspectos de la realidad que resultan relevantes para responder una determinada pregunta. Por ejemplo, si deseamos estimar la probabilidad de lluvia, probablemente no necesitemos conocer la posición exacta de cada molécula de aire de la atmósfera. Basta con describir algunas variables agregadas como la presión, la temperatura y la humedad.

En otras palabras, aprender consiste en ignorar una enorme cantidad de detalles para conservar únicamente la información más importante.

---

## El costo de simplificar

Toda simplificación implica una pérdida de información.

Supongamos que tomamos una fotografía de muy alta resolución. Posteriormente reducimos su tamaño para poder enviarla por internet. La nueva imagen ocupa mucho menos espacio. Sin embargo, algunos detalles desaparecen. Aunque ambas imágenes representan el mismo paisaje, una contiene menos información que la otra. Los modelos estadísticos funcionan de manera muy similar. Partimos de una realidad extremadamente rica en información y construimos una versión mucho más simple que conserva únicamente aquello que consideramos importante.

La siguiente figura resume esta idea.

```text
Realidad
   │
   │ (observación)
   ▼
Datos
   │
   │ (aprendizaje)
   ▼
Modelo
   │
   │ (predicción)
   ▼
Decisiones
```

A medida que avanzamos por esta unidad veremos que cada una de estas transformaciones implica pérdidas, aproximaciones e incertidumbre.

---

# La idea central de esta unidad

En las unidades anteriores estudiamos cómo estimar probabilidades y cómo ajustar distribuciones a partir de datos.

Ahora cambiaremos ligeramente el punto de vista. Ya no nos preguntaremos únicamente: 

> ¿Cuál es la mejor distribución para estos datos?

Sino una pregunta mucho más profunda:

> ¿Qué significa construir un buen modelo?

Responder esta pregunta requiere comprender varios conceptos fundamentales:

* qué información contienen realmente los datos;
* por qué nunca conocemos la población completa;
* cómo aparecen distintos tipos de error;
* qué significa que un modelo sea demasiado simple o demasiado complejo;
* cómo medir la distancia entre un modelo y la realidad;
* y, finalmente, qué significa generalizar.

Todos estos conceptos forman parte de una misma idea.

---

## Aprender como construcción de un modelo

Cuando una persona aprende a reconocer árboles, no memoriza cada árbol que ha visto durante su vida. Lo que hace es construir una representación mental. Después de observar cientos de árboles diferentes comienza a identificar ciertas características comunes:

* poseen un tronco;
* presentan ramas;
* tienen hojas o agujas;
* crecen desde el suelo.

Gracias a esa representación es capaz de reconocer árboles completamente nuevos que nunca había visto. Esto mismo ocurre en aprendizaje automático. Un algoritmo no pretende memorizar todos los ejemplos del entrenamiento. Su objetivo consiste en construir una representación suficientemente general para reconocer nuevos ejemplos en el futuro. En consecuencia, aprender no significa almacenar datos. Aprender significa construir una representación que permita explicar observaciones pasadas y realizar predicciones futuras.

Esta idea será el hilo conductor de toda la unidad.

---

## Una perspectiva desde la teoría de la información

Existe otra forma de interpretar exactamente el mismo proceso.

Podemos pensar que cada observación aporta cierta cantidad de información acerca del fenómeno que estamos estudiando. A medida que llegan nuevos datos, nuestro conocimiento aumenta. Sin embargo, nunca almacenamos toda esa información de manera explícita.

En lugar de ello, construimos un modelo mucho más compacto capaz de resumirla. Desde esta perspectiva, aprender puede interpretarse como un proceso de compresión de información.

Los datos contienen una enorme cantidad de detalles. El modelo intenta conservar únicamente aquellos que resultan necesarios para explicar el fenómeno. Esta interpretación conecta de forma natural con la teoría de la información estudiada en unidades anteriores. La entropía medía la incertidumbre de un sistema. Ahora veremos que aprender consiste precisamente en reducir parte de esa incertidumbre mediante la construcción de modelos.

---

## Lo que estudiaremos en esta unidad

A lo largo de este capítulo responderemos progresivamente la pregunta inicial.

Comenzaremos estudiando qué es realmente un modelo y por qué necesitamos construirlos. Posteriormente analizaremos las distintas fuentes de error que aparecen durante el aprendizaje. Después aprenderemos cómo medir la diferencia entre un modelo y la realidad mediante conceptos provenientes de la teoría de la información, como la divergencia de Kullback-Leibler y la entropía cruzada. Finalmente estudiaremos por qué algunos modelos aprenden demasiado, otros aprenden muy poco y cómo encontrar un equilibrio entre ambos extremos.

Al terminar esta unidad podremos interpretar gran parte del aprendizaje automático desde una única perspectiva:

> **Aprender consiste en construir una representación simplificada de la realidad utilizando únicamente la información contenida en los datos disponibles.**

Esta idea, aparentemente sencilla, servirá como fundamento para comprender los algoritmos de aprendizaje que estudiaremos en las siguientes unidades.

---

# ¿Qué es un modelo?

## La necesidad de representar la realidad

En la sección anterior planteamos una pregunta fundamental:

> **¿Qué significa realmente aprender?**

Encontramos una primera respuesta: aprender consiste en construir una representación simplificada de la realidad.

Ahora debemos profundizar un poco más en esa idea.

¿Qué significa exactamente "representar" la realidad? ¿Por qué no utilizamos directamente la realidad tal como es? 

La respuesta es sencilla: porque la realidad es demasiado compleja. Ningún ser humano, ninguna ecuación y ningún computador pueden almacenar absolutamente toda la información de un fenómeno físico. Por esta razón construimos modelos.

---

## Una representación, no una copia

Cuando observamos un mapa de una ciudad sabemos que dicho mapa no es la ciudad. En él no aparecen las personas caminando, los árboles moviéndose con el viento ni cada uno de los edificios con todos sus detalles. Sin embargo, el mapa resulta extraordinariamente útil.

¿Por qué? Porque conserva únicamente la información necesaria para cumplir un propósito.

Si nuestro objetivo consiste en desplazarnos desde un punto hasta otro, basta con conocer las calles y las intersecciones.

Toda la información restante puede eliminarse. Un plano arquitectónico funciona de manera similar. No representa los colores reales de las paredes ni la textura de los materiales. Representa dimensiones, ubicaciones y relaciones espaciales.

Un globo terráqueo tampoco intenta reproducir cada montaña, cada árbol o cada edificio del planeta. Su propósito consiste únicamente en representar la forma general de la Tierra y la ubicación relativa de los continentes. 

En todos estos ejemplos ocurre exactamente lo mismo.

> Un modelo no intenta copiar la realidad; intenta conservar únicamente aquella información que resulta útil para responder una determinada pregunta.

---

## Modelar consiste en elegir

Construir un modelo implica tomar decisiones.

Supongamos que deseamos modelar el movimiento de un automóvil. Podríamos considerar cientos de variables:

* masa del vehículo,
* potencia del motor,
* presión de las llantas,
* resistencia del aire,
* temperatura ambiente,
* humedad,
* inclinación de la carretera,
* desgaste de los neumáticos,
* dirección del viento,
* vibraciones del motor.

Sin embargo, dependiendo del problema que deseemos resolver, muchas de estas variables pueden resultar irrelevantes. Si únicamente queremos estimar el tiempo necesario para recorrer una autopista, probablemente basten variables como la velocidad promedio y la distancia recorrida. Las demás pueden ignorarse sin afectar significativamente el resultado. Modelar consiste precisamente en decidir qué información conservar y qué información descartar.

En consecuencia, ningún modelo es completamente objetivo. Siempre refleja las decisiones tomadas por quien lo construye.

---

## Todos los modelos son aproximaciones

Existe una frase muy conocida del estadístico George Box:

> **"Todos los modelos están equivocados, pero algunos son útiles."**

Esta afirmación puede parecer contradictoria.

¿Cómo puede ser útil algo que sabemos que está equivocado?

La respuesta aparece cuando comprendemos la verdadera naturaleza de un modelo. Un modelo nunca reproduce exactamente la realidad. Siempre introduce simplificaciones. Siempre ignora algunos detalles. Siempre comete errores. Sin embargo, puede ser suficientemente preciso para responder correctamente la pregunta que nos interesa. 

Por ejemplo, cuando calculamos la trayectoria de un balón solemos utilizar las ecuaciones de la mecánica clásica. Estas ecuaciones ignoran muchos fenómenos:

* pequeñas turbulencias del aire,
* deformaciones del balón,
* variaciones locales de la gravedad,
* efectos relativistas.

A pesar de ello, las predicciones resultan extraordinariamente buenas. El modelo no es perfecto. Simplemente es suficientemente bueno para el problema que deseamos resolver.

---

## El propósito define el modelo

No existe un modelo universalmente correcto. Existe un modelo adecuado para cada propósito. Supongamos que deseamos estudiar un bosque.Dependiendo del objetivo necesitaremos modelos completamente diferentes. Si queremos conocer la distribución de especies, construiremos un modelo biológico. Si deseamos estimar el crecimiento de los árboles, utilizaremos un modelo ecológico. Si queremos calcular la propagación de un incendio, necesitaremos un modelo físico. Si pretendemos planificar senderos turísticos, probablemente construiremos un modelo geográfico.

La realidad observada es exactamente la misma. Lo único que cambia es la pregunta que intentamos responder. En consecuencia, un modelo siempre debe evaluarse con respecto a su propósito. No tiene sentido preguntar si un modelo es "verdadero". La pregunta correcta es otra:

> **¿Este modelo resulta útil para responder la pregunta que estamos formulando?**

---

## Variables y relaciones

Todo modelo intenta describir relaciones entre variables.

Por ejemplo, en Física aprendemos que la distancia recorrida por un objeto depende de su velocidad y del tiempo.

Podemos escribir

$$
d=v\,t
$$

Esta sencilla ecuación constituye un modelo. No describe absolutamente todo el movimiento del universo. Describe únicamente la relación entre tres variables bajo determinadas condiciones.

De forma similar, la Ley de Ohm

$$
V=RI
$$

es otro modelo.

La ecuación de los gases ideales

$$
PV=nRT
$$

también es un modelo.

Incluso una receta de cocina puede interpretarse como un modelo. Relaciona cantidades de ingredientes con un resultado esperado.

En todos los casos encontramos la misma idea:

> Un modelo establece relaciones entre variables para explicar o predecir un fenómeno.

---

## Los modelos estadísticos

Hasta ahora hemos hablado de modelos en un sentido muy general.

En este curso nos interesan especialmente los modelos estadísticos. La diferencia principal respecto a muchos modelos físicos consiste en que aceptan explícitamente la existencia de incertidumbre. Supongamos que deseamos estimar el peso de una persona a partir de su estatura. No existe una ecuación exacta que permita calcularlo. Dos personas con la misma estatura pueden tener pesos completamente diferentes. En este caso el modelo no produce una respuesta única. Produce una distribución de probabilidad.

En lugar de afirmar

> "Una persona de 1.75 m pesa exactamente 72 kg"

el modelo responde algo mucho más realista:

> "Una persona de 1.75 m tiene una mayor probabilidad de pesar alrededor de 72 kg, aunque otros valores también son posibles."

Esta diferencia es fundamental. Los modelos estadísticos no eliminan la incertidumbre. La describen.

---

## Un modelo como una función

Desde un punto de vista matemático podemos representar un modelo mediante una función.

Supongamos que disponemos de un conjunto de variables de entrada

$$
X=(x_1,x_2,\ldots,x_n)
$$

y deseamos predecir una determinada salida

$$
Y.
$$

Podemos escribir

$$
Y=f(X).
$$

La función

$$ 
f
$$

representa el modelo. Dependiendo del problema, esta función puede ser:

* una recta,
* un polinomio,
* una distribución de probabilidad,
* un árbol de decisión,
* una máquina de soporte vectorial,
* una red neuronal profunda.

Aunque estas herramientas parezcan muy diferentes, todas cumplen exactamente el mismo propósito. Intentan aproximar la relación existente entre las variables de entrada y las variables de salida.

---

## El modelo verdadero

Llegamos ahora a una idea muy importante. En la mayoría de los problemas reales existe una relación desconocida entre las variables. Podemos imaginarla como una función desconocida

$$
f^\star(X).
$$

El símbolo

$$
^\star
$$

se utiliza frecuentemente para representar el modelo verdadero o la función real que gobierna el fenómeno. El problema es que nunca conocemos esa función. Si la conociéramos, el aprendizaje automático dejaría de tener sentido. Todo el esfuerzo del aprendizaje consiste precisamente en construir una aproximación

$$
\hat f(X)
$$

que se parezca lo más posible a

$$
f^\star(X).
$$

Aquí aparece una de las ideas más importantes de toda la teoría del aprendizaje.

```text
Realidad
      │
      ▼
Función verdadera  f*(X)
      │
      │ (desconocida)
      ▼
Datos observados
      │
      ▼
Algoritmo de aprendizaje
      │
      ▼
Modelo aprendido  f^(X)
```

El algoritmo nunca observa directamente la función verdadera.  Únicamente observa ejemplos producidos por ella. A partir de esos ejemplos intenta reconstruir una aproximación. Toda la teoría del aprendizaje estadístico gira alrededor de esta idea.

---

## Un modelo es conocimiento comprimido

Podemos terminar esta sección con una interpretación diferente. Supongamos que observamos un millón de ejemplos de un fenómeno. Una posibilidad sería almacenar el millón de observaciones. Otra posibilidad consiste en construir un modelo que resuma toda esa información mediante unas pocas ecuaciones o unos pocos parámetros.

Esta segunda estrategia resulta mucho más eficiente. El modelo funciona como una forma de compresión. No almacena los datos. Almacena las relaciones que existen entre ellos. Esta será una idea recurrente durante toda la unidad. Aprender no significa memorizar. Aprender significa descubrir una representación suficientemente compacta para explicar una gran cantidad de observaciones.

En las próximas secciones veremos que esta representación nunca es perfecta. Siempre contiene errores.

La pregunta ya no será si un modelo comete errores. La pregunta será:

> **¿De dónde provienen esos errores y cómo podemos cuantificarlos?**

Miremos este enlace a un libro que ayudará a entender ese concepto de la compresión de la información: [Libro de conocimiento comprimido](./modelo_conocimiento_comprimido.ipynb)

---

# El problema fundamental del aprendizaje

En las secciones anteriores comprendimos que aprender consiste en construir un modelo y que dicho modelo no es una copia de la realidad, sino una representación simplificada de ella.

Sin embargo, aún queda una pregunta por responder.

> **Si disponemos de algoritmos cada vez más sofisticados y computadores cada vez más potentes, ¿por qué nunca logramos aprender exactamente la realidad?**

La respuesta no depende de las limitaciones tecnológicas. Incluso si dispusiéramos de capacidad de cómputo ilimitada, seguiríamos enfrentando un problema mucho más profundo. El conocimiento que obtenemos siempre es incompleto. La información que poseemos siempre es limitada. Y, en consecuencia, todo modelo aprendido será necesariamente una aproximación. Comprender por qué ocurre esto constituye una de las ideas centrales del aprendizaje estadístico.

---

## La realidad es inaccesible

Imaginemos que deseamos construir un modelo que describa el comportamiento de una población.

Por ejemplo:

* la estatura de todos los habitantes de un país;
* el tiempo que tarda un paciente en recuperarse;
* el consumo eléctrico de una ciudad;
* la probabilidad de que una persona compre un determinado producto.

Idealmente nos gustaría observar absolutamente todos los individuos. Si pudiéramos hacerlo conoceríamos exactamente la distribución del fenómeno. Sin embargo, esto casi nunca es posible. Las poblaciones suelen ser enormes. En algunos casos incluso cambian continuamente con el tiempo. En otros casos son, en la práctica, infinitas. Como consecuencia, nunca observamos la realidad completa. Únicamente observamos una pequeña parte de ella.

---

## La población y la muestra

La Estadística distingue claramente dos conceptos fundamentales.

La **población** corresponde al conjunto completo de todos los individuos o eventos que deseamos estudiar.

La **muestra** corresponde únicamente al subconjunto de observaciones que realmente logramos obtener.

Podemos representarlo de la siguiente manera.

```text
Población completa
┌───────────────────────────────┐
│ • • • • • • • • • • • • • • • │
│ • • • • • • • • • • • • • • • │
│ • • • • • • • • • • • • • • • │
└───────────────────────────────┘
              │
              │ Muestreo
              ▼
┌───────────────────────────────┐
│ • • • • • • • • • •           │
└───────────────────────────────┘
          Muestra
```

Todo el aprendizaje estadístico parte únicamente de la muestra. La población permanece desconocida. Esta simple observación tiene consecuencias profundas.

---

## Aprendemos a partir de evidencia incompleta

Supongamos que deseamos conocer la estatura promedio de todos los habitantes de Colombia. Sería imposible medir uno por uno a todos los ciudadanos. Lo que hacemos es seleccionar una muestra representativa. A partir de ella calculamos un promedio. Ese promedio constituye una estimación. No conocemos el valor real. Conocemos únicamente una aproximación. Lo mismo ocurre cuando entrenamos un modelo de aprendizaje automático. Nunca disponemos de todos los ejemplos posibles. Disponemos únicamente del conjunto de entrenamiento.

Nuestro modelo aprende exclusivamente a partir de esa evidencia parcial. En otras palabras,

> **todo algoritmo aprende a partir de información incompleta.**

---

## Aprender significa inferir

Aquí aparece una palabra que resume gran parte de esta unidad:

**inferir**.

Inferir significa obtener conclusiones acerca de algo que no observamos directamente.

Por ejemplo:
```text
observamos algunos pacientes

↓

inferimos el comportamiento de la enfermedad.
```

```text
Observamos algunos consumidores

↓

inferimos el comportamiento del mercado.
```

```text
Observamos miles de fotografías

↓

inferimos cómo reconocer objetos nuevos.
```

```text
Observamos algunos millones de palabras

↓

inferimos las reglas de un idioma.
```

En todos estos ejemplos ocurre exactamente el mismo proceso. Los datos observados constituyen únicamente evidencia. El objetivo del aprendizaje consiste en extrapolar esa evidencia hacia situaciones nuevas.

---

## La ilusión de conocer la realidad

Con frecuencia olvidamos que los datos que observamos no son la realidad. Son únicamente mediciones de ella.

Imaginemos un sensor de temperatura. Cada medición depende de numerosos factores:

* precisión del sensor;
* resolución del instrumento;
* ruido electrónico;
* condiciones ambientales;
* errores de calibración.

Cuando registramos una temperatura de

$$
24.3^\circ C
$$

no estamos observando exactamente la temperatura real. Estamos observando una medición afectada por pequeñas incertidumbres. Lo mismo ocurre prácticamente con cualquier dato. Las bases de datos contienen errores. Las personas responden incorrectamente algunas encuestas. Los sensores presentan ruido. Los instrumentos tienen precisión finita. Incluso los experimentos científicos contienen incertidumbre.

Por esta razón,

> **los datos nunca constituyen una descripción perfecta de la realidad.**

---

## La función verdadera permanece oculta

En la sección anterior representamos el fenómeno mediante una función desconocida

$$
f^\star(x).
$$

Ahora podemos comprender mejor su significado.

Supongamos que realmente existe una relación entre una variable de entrada

$$
x
$$

y una variable de salida

$$
y.
$$

Podemos escribir

$$
y=f^\star(x).
$$

Sin embargo, nunca observamos directamente

$$
f^\star.
$$

Únicamente observamos algunos pares

$$
(x_i,y_i).
$$

Por ejemplo,

```text
Edad        Presión arterial

32          118
45          126
51          135
60          141
67          150
```

A partir de unos pocos ejemplos intentamos reconstruir una función que explique todos los posibles casos.

Nuestro modelo constituye únicamente una aproximación.

---

## El verdadero desafío

Podría parecer que basta con recolectar una cantidad enorme de datos. Sin embargo, el problema continúa existiendo. Aunque observáramos un millón de ejemplos, seguiríamos sin conocer la totalidad de los casos posibles. Siempre existirán situaciones nuevas.

* Nuevos pacientes.
* Nuevas condiciones climáticas.
* Nuevas fotografías.
* Nuevos textos.
* Nuevos usuarios.

El aprendizaje automático nunca trabaja sobre un conjunto cerrado de situaciones. Siempre debe prepararse para enfrentar ejemplos que todavía no existen. Esta idea recibe el nombre de **generalización**, y se convertirá en uno de los conceptos más importantes de esta unidad.

---

## El conocimiento siempre es provisional

Existe otra consecuencia interesante. Cada nuevo dato puede modificar el modelo. Supongamos que entrenamos un sistema para reconocer aves utilizando diez mil fotografías. Posteriormente obtenemos otras diez mil imágenes provenientes de una región diferente del planeta. Probablemente el modelo cambie. Su conocimiento aumenta. 
Su representación de la realidad mejora. Esto significa que el conocimiento aprendido nunca debe considerarse definitivo. Siempre depende de la evidencia disponible. Esta idea resulta completamente coherente con la interpretación bayesiana estudiada en la unidad anterior. Cada nueva observación constituye evidencia adicional que modifica nuestro conocimiento.

Desde esta perspectiva, el aprendizaje nunca termina. Simplemente continúa refinando el modelo a medida que aparecen nuevas observaciones.

---

## ¿Por qué los modelos cometen errores?

Llegamos ahora a una pregunta fundamental. Si todo modelo aprende únicamente a partir de información parcial, ¿de dónde provienen realmente sus errores? Podría parecer que todos los errores tienen una misma causa. Sin embargo, esto no es cierto. Existen varias fuentes de error completamente diferentes. 

* Algunas aparecen porque observamos únicamente una muestra. 
* Otras aparecen porque el modelo elegido no representa adecuadamente el fenómeno.
* Y otras aparecen porque el propio fenómeno contiene incertidumbre que ningún modelo puede eliminar.

Distinguir estas fuentes resulta esencial para comprender el aprendizaje estadístico. Durante las próximas secciones estudiaremos cada una de ellas por separado.

---

## Tres preguntas que acompañarán el resto de la unidad

Todo lo que estudiaremos a partir de este punto puede resumirse mediante tres preguntas.

**Primera pregunta**

¿Estamos aprendiendo a partir de una muestra suficientemente representativa?

Si la respuesta es negativa, aparecerá el **error de muestreo**.

---

**Segunda pregunta**

¿Nuestro modelo tiene la capacidad suficiente para representar el fenómeno?

Si la respuesta es negativa, aparecerá el **error estructural**.

---

**Tercera pregunta**

¿Incluso con un buen modelo y una buena muestra seguirá existiendo incertidumbre?

La respuesta es sí.

Muchos fenómenos contienen una componente aleatoria que ningún algoritmo puede eliminar.

Esta componente recibe el nombre de **incertidumbre residual**.

---

Estas tres ideas constituyen el fundamento del aprendizaje estadístico moderno.

Comprenderlas permitirá responder una de las preguntas más importantes de toda la inteligencia artificial:

> **¿Qué parte del error puede reducirse aprendiendo más y qué parte del error nunca podrá eliminarse?**

La respuesta comenzará a construirse en las siguientes secciones.

---

# Modelos empíricos

En las secciones anteriores comprendimos que aprender consiste en construir un modelo a partir de una cantidad limitada de observaciones. Sin embargo, todavía no hemos respondido una pregunta importante.

> **¿Cómo construimos realmente ese modelo?**

Existen muchas formas de hacerlo. La más sencilla consiste en dejar que los propios datos describan directamente el fenómeno observado. Este tipo de representación recibe el nombre de **modelo empírico**. Antes de introducir ecuaciones, distribuciones de probabilidad o redes neuronales, resulta conveniente comprender esta idea, ya que constituye el punto de partida de prácticamente toda la Estadística.

---

## Aprender observando

Desde pequeños aprendemos muchas cosas simplemente observando. Un niño no necesita conocer las leyes de la gravedad para comprender que los objetos caen. Después de observar cientos de veces el mismo fenómeno, comienza a esperar que vuelva a ocurrir. Su conocimiento proviene directamente de la experiencia. No utiliza ecuaciones. No realiza cálculos. Simplemente acumula observaciones. Los modelos empíricos funcionan exactamente de la misma manera. No parten de una teoría previa. No suponen cómo debería comportarse el fenómeno. Únicamente registran lo que realmente ocurrió.

---

## La experiencia como modelo

Supongamos que deseamos conocer la probabilidad de obtener cara al lanzar una moneda. Realizamos diez lanzamientos y obtenemos

```text
Cara
Cara
Sello
Cara
Cara
Cara
Sello
Cara
Cara
Cara
```

La forma más sencilla de estimar la probabilidad consiste en calcular la frecuencia observada.

Tenemos

* 8 caras.
* 2 sellos.

Por tanto,

$$
\hat P(\text{cara})
=
\frac{8}{10}
=
0.8
$$

y

$$
\hat P(\text{sello})
=
\frac{2}{10}
=
0.2
$$

No hemos supuesto absolutamente nada acerca de la moneda. No hemos utilizado ninguna distribución. No hemos construido ninguna ecuación. Simplemente dejamos que los datos hablaran por sí mismos. Este es precisamente el espíritu de un modelo empírico.

---

## La distribución empírica

Generalizando la idea anterior, si una variable puede tomar distintos valores

$$
x_1,x_2,\ldots,x_k,
$$

podemos estimar su probabilidad mediante las frecuencias observadas.

Si el valor

$$
x_i
$$

aparece

$$
n_i
$$

veces dentro de una muestra de tamaño

$$
N,
$$

la distribución empírica queda definida por

$$
\hat P(x_i)
=
\frac{n_i}{N}.
$$

Esta distribución constituye la descripción más directa posible de los datos observados. No intenta suavizar la información. No intenta interpretarla. Simplemente refleja exactamente aquello que fue observado.

---

### Un ejemplo sencillo

Supongamos que preguntamos a veinte estudiantes cuál es su medio de transporte habitual para llegar a la universidad.

Obtenemos los siguientes resultados.

| Medio | Frecuencia |
|---------|-----------:|
| Automóvil | 6 |
| Bus | 8 |
| Bicicleta | 3 |
| Caminando | 3 |

La distribución empírica será

| Medio | Probabilidad |
|---------|-------------:|
| Automóvil | 0.30 |
| Bus | 0.40 |
| Bicicleta | 0.15 |
| Caminando | 0.15 |

Este modelo resume toda la información contenida en las observaciones. Si un nuevo estudiante fuera elegido al azar, nuestra mejor estimación de su medio de transporte sería precisamente esta distribución.

---

## El histograma como modelo empírico

Cuando las variables son continuas, como la estatura, el peso o la temperatura, resulta imposible asignar una probabilidad distinta a cada valor posible. En estos casos agrupamos los datos en intervalos.

Por ejemplo,

```text
150–160 cm

160–170 cm

170–180 cm

180–190 cm
```

Contamos cuántas observaciones pertenecen a cada intervalo y construimos un histograma. Aunque solemos pensar en el histograma únicamente como una gráfica, en realidad constituye un modelo estadístico. Describe cómo se distribuyen los datos utilizando únicamente las frecuencias observadas. En consecuencia, un histograma puede interpretarse como una representación empírica de una distribución de probabilidad.

---

## Ventajas de los modelos empíricos

Los modelos empíricos presentan varias ventajas importantes. La primera consiste en que requieren muy pocos supuestos. No necesitamos asumir que los datos siguen una distribución Normal, Poisson o Gamma. Simplemente observamos los datos.

Otra ventaja consiste en que describen exactamente la muestra observada. No introducen aproximaciones adicionales. Toda la información disponible permanece representada.

Además, su construcción resulta extremadamente sencilla. Basta con contar frecuencias o construir histogramas. Por esta razón constituyen el punto de partida natural en cualquier análisis exploratorio de datos. Antes de ajustar modelos complejos, siempre conviene observar primero cómo son realmente los datos.

---

## La otra cara de la moneda

Sin embargo, los modelos empíricos también presentan limitaciones importantes. Imaginemos nuevamente la moneda. Supongamos ahora que únicamente realizamos dos lanzamientos.

Obtenemos

```text
Cara
Cara
```

La distribución empírica sería

$$
\hat P(\text{cara})=1
$$

y

$$
\hat P(\text{sello})=0.
$$

¿Significa esto que la moneda nunca producirá sello?

Por supuesto que no. Simplemente disponemos de muy poca información.  Nuestro modelo refleja únicamente aquello que fue observado. Nada más. Esta limitación aparece continuamente cuando las muestras son pequeñas.

---

## El problema de la memoria

Existe otra dificultad aún más importante. Supongamos que registramos diariamente la temperatura de una ciudad durante cincuenta años. Obtendremos más de dieciocho mil observaciones. Un modelo empírico debería conservarlas todas. Si el fenómeno contiene millones de datos, el modelo necesitará almacenar millones de observaciones. En consecuencia, la complejidad del modelo crece continuamente con el tamaño de la base de datos.

Esto puede convertirse rápidamente en un problema computacional.

---

## El problema de la generalización

Hasta ahora los modelos empíricos únicamente describen aquello que ya observaron. Pero el objetivo del aprendizaje automático es mucho más ambicioso. Queremos responder preguntas sobre situaciones nuevas. Supongamos que conocemos la distribución empírica de las estaturas de mil estudiantes. Posteriormente llega un estudiante cuya estatura es

$$
173.42\text{ cm}.
$$

Es posible que nunca hayamos observado exactamente ese valor. ¿Qué probabilidad deberíamos asignarle? Los modelos empíricos tienen dificultades para responder este tipo de preguntas. Describen muy bien el pasado. Pero generalizan poco hacia situaciones no observadas.

Esta limitación se vuelve especialmente importante cuando trabajamos con variables continuas o espacios de alta dimensión.

---

## El crecimiento exponencial de los datos

Imaginemos ahora que no observamos una sola variable sino diez.

Por ejemplo,

* edad,
* estatura,
* peso,
* presión arterial,
* frecuencia cardíaca,
* colesterol,
* temperatura,
* glucosa,
* actividad física,
* horas de sueño.

Cada nueva variable incrementa enormemente el número de combinaciones posibles. Muy rápidamente descubrimos que resulta prácticamente imposible observar todas ellas. Este fenómeno recibe el nombre de **maldición de la dimensionalidad** y aparecerá con frecuencia en aprendizaje automático. Los modelos puramente empíricos sufren especialmente este problema. Necesitan enormes cantidades de datos para cubrir todas las combinaciones posibles.

---

## La necesidad de resumir

Llegamos así a una conclusión importante. Los modelos empíricos describen fielmente la información observada. Sin embargo, requieren almacenar grandes cantidades de datos, generalizan con dificultad, y necesitan muestras cada vez mayores a medida que aumenta la complejidad del problema.

Esto nos lleva naturalmente a formular una nueva pregunta.

> **¿Es posible describir millones de observaciones utilizando únicamente unas pocas cantidades?**

La respuesta es afirmativa. En lugar de almacenar todos los datos, podemos resumir su comportamiento mediante unos pocos parámetros. Esta idea constituye el fundamento de los **modelos paramétricos**, que estudiaremos en la siguiente sección.

En cierto sentido, los modelos paramétricos representan una forma de compresión del conocimiento. No almacenan cada observación. Almacenan únicamente aquello que consideran esencial para describir el fenómeno. Esta idea conectará posteriormente con la teoría de la información y con una interpretación mucho más profunda del aprendizaje estadístico.

---

# Modelos paramétricos

En la sección anterior estudiamos los modelos empíricos y descubrimos que constituyen la forma más directa de describir un conjunto de observaciones.

En ellos, los propios datos representan el modelo. Sin embargo, también encontramos una dificultad importante. A medida que aumenta el número de observaciones, el modelo crece indefinidamente. Si deseamos describir millones de datos, deberíamos almacenar millones de observaciones. Esto plantea una nueva pregunta.

> **¿Es posible describir un fenómeno complejo utilizando únicamente unas pocas cantidades?**

La respuesta a esta pregunta constituye uno de los pilares de la Estadística moderna. En lugar de almacenar toda la información disponible, intentaremos resumir su comportamiento mediante un pequeño conjunto de parámetros. Este tipo de representación recibe el nombre de **modelo paramétrico**.

---

## De los datos al modelo

Supongamos que registramos la estatura de mil personas. Un modelo empírico conservaría las mil mediciones. Podríamos construir un histograma o una distribución de frecuencias. Sin embargo, después de observar la forma de los datos, notamos algo interesante. Las estaturas parecen concentrarse alrededor de un valor promedio. Además, los valores extremos aparecen con mucha menor frecuencia. La distribución presenta una forma aproximadamente simétrica. Este comportamiento recuerda inmediatamente a una distribución Normal. En lugar de almacenar las mil observaciones, podríamos describir todo el conjunto mediante únicamente dos parámetros:

* la media

$$
\mu
$$

* la desviación estándar

$$
\sigma
$$

A partir de estos dos números podemos reconstruir una aproximación muy razonable del comportamiento de toda la población. Esta es precisamente la idea fundamental de un modelo paramétrico.

---

## ¿Qué es un parámetro?

Un parámetro es una cantidad que caracteriza el comportamiento de un modelo. Dependiendo del tipo de distribución, los parámetros pueden tener interpretaciones diferentes.

Por ejemplo:

Distribución Bernoulli

$$
p
$$

representa la probabilidad de éxito.

---

Distribución Poisson

$$
\lambda
$$

representa el número esperado de eventos por unidad de tiempo.

---

Distribución Normal

$$
\mu
$$

indica el valor promedio.

$$
\sigma
$$

describe la dispersión de los datos.

---

Distribución Gamma

sus parámetros determinan simultáneamente la forma y la escala de la distribución.

En todos los casos ocurre exactamente lo mismo. Los parámetros resumen la información más importante del fenómeno.

---

## Una enorme reducción de información

Imaginemos que registramos un millón de mediciones.

Podemos representar esa información de dos maneras.

**Modelo empírico**

```text
1 000 000 observaciones
```

---

**Modelo Normal**

```text
μ = 18.4

σ = 2.7
```

Toda la información ha sido resumida mediante únicamente dos números. Naturalmente, durante este proceso se pierde cierta información. Sin embargo, si la distribución Normal representa adecuadamente el fenómeno, la pérdida será pequeña. Esta observación resulta extraordinariamente importante.

> Un modelo paramétrico puede entenderse como un mecanismo de compresión de información.

---

## Compresión sin memorizar

Existe una diferencia fundamental entre almacenar datos y aprender un modelo. Supongamos que deseamos describir la trayectoria diaria de la temperatura durante un año. Una posibilidad consiste en almacenar las 365 mediciones. Otra posibilidad consiste en descubrir que la temperatura sigue aproximadamente un comportamiento periódico. Entonces bastaría una función del tipo

$$
T(t)=A\sin(\omega t+\phi)+c
$$

En lugar de almacenar cientos de observaciones, almacenamos únicamente unos pocos parámetros:

* amplitud,
* frecuencia,
* fase,
* nivel medio.

El modelo ya no recuerda cada medición. Recuerda la estructura que explica las mediciones. Esta diferencia constituye uno de los principios fundamentales del aprendizaje automático.

---

## Familias de modelos

Cuando hablamos de modelos paramétricos no nos referimos a una única ecuación.

Hablamos de una familia completa de posibles modelos.

Por ejemplo,

la distribución Normal puede escribirse como

$$
N(\mu,\sigma)
$$

Cada elección distinta de

$$
\mu
$$

y

$$
\sigma
$$

produce una distribución diferente.

Podemos imaginarlo como una enorme colección de curvas posibles. El aprendizaje consiste simplemente en encontrar cuáles parámetros producen la curva que mejor representa los datos observados.

---

## El espacio de modelos

Esta idea permite introducir un concepto muy útil.  Antes de observar los datos, existen muchas posibilidades. Por ejemplo, para una distribución Normal, la media podría ser

10,

20,

30,

o cualquier otro valor.

La desviación estándar también puede tomar numerosos valores. Cada combinación representa un modelo distinto. Podemos imaginar un enorme espacio de modelos posibles.

```text
                Espacio de modelos

 N(10,2)

 N(12,5)

 N(15,3)

 N(18,4)

 N(20,6)

        ...

        ↓

Los datos seleccionan uno de ellos.
```

Desde esta perspectiva, aprender consiste en buscar, dentro de una familia de modelos, aquel cuyos parámetros describen mejor la evidencia disponible.

---

## Aprender parámetros

En la unidad anterior estudiamos precisamente cómo realizar esta búsqueda.

Maximum Likelihood responde a la pregunta:

> ¿Qué parámetros hacen que los datos observados sean lo más probables posible?

La inferencia bayesiana responde otra pregunta ligeramente diferente:

> ¿Qué distribución de probabilidad debemos asignar a los posibles valores de los parámetros?

Ambos enfoques buscan exactamente el mismo objetivo. Encontrar el modelo que mejor representa los datos. La diferencia radica en cómo interpretan la incertidumbre asociada a dichos parámetros.

---

## Ventajas de los modelos paramétricos

Los modelos paramétricos poseen varias ventajas importantes.

En primer lugar, requieren muy poca memoria. Una enorme cantidad de observaciones puede resumirse mediante unos pocos parámetros.

En segundo lugar, permiten realizar predicciones para valores que nunca fueron observados.

Por ejemplo,

aunque nunca hayamos observado exactamente una persona de

173.42 cm,

la distribución Normal puede asignarle una probabilidad. Esto constituye una enorme ventaja frente a los modelos puramente empíricos. Finalmente, muchos parámetros poseen una interpretación física o estadística muy clara. La media representa el comportamiento promedio. La desviación estándar representa la dispersión. La tasa de Poisson representa una frecuencia de ocurrencia. Esta interpretabilidad facilita considerablemente el análisis de los fenómenos.

---

## El precio de resumir

Sin embargo, la compresión tiene un costo. Cuando resumimos un millón de datos mediante únicamente dos parámetros, estamos suponiendo que la distribución elegida describe correctamente el fenómeno.

Si esta hipótesis resulta incorrecta, el modelo puede producir errores importantes. Supongamos que intentamos describir una distribución claramente asimétrica mediante una distribución Normal. Aunque conozcamos perfectamente los valores de

$$
\mu
$$

y

$$
\sigma,
$$

el modelo seguirá siendo inadecuado. El problema ya no se encuentra en los parámetros. El problema aparece porque elegimos una familia de modelos incorrecta. Más adelante veremos que esta situación recibe el nombre de **error estructural**.

---

## Elegir un modelo también es una hipótesis

Cada vez que seleccionamos una distribución estamos formulando una hipótesis acerca del comportamiento del fenómeno. Cuando utilizamos una distribución Normal estamos suponiendo, implícitamente, que los datos presentan una forma aproximadamente simétrica. Cuando utilizamos una distribución Poisson estamos suponiendo que los eventos ocurren de manera independiente y con una tasa aproximadamente constante. Cuando utilizamos una distribución Exponencial estamos suponiendo que los tiempos entre eventos siguen un determinado comportamiento. Estas hipótesis rara vez son completamente ciertas.

Sin embargo, si describen razonablemente bien el fenómeno, el modelo puede resultar extraordinariamente útil.

---

## Los modelos como mecanismos de explicación

Existe una interpretación aún más profunda. Un modelo no solo resume datos. También intenta explicar por qué esos datos presentan determinado comportamiento.

Por ejemplo, la distribución Normal aparece naturalmente cuando muchas pequeñas causas independientes contribuyen simultáneamente al resultado observado. La distribución Poisson describe procesos donde contamos eventos discretos. La distribución Exponencial aparece cuando modelamos tiempos de espera.

En consecuencia, elegir un modelo también significa proponer una explicación acerca del mecanismo que genera los datos.

---

# Hacia una interpretación informacional

Podemos resumir las ideas anteriores mediante el siguiente esquema.

```text
Realidad

        ↓

Observaciones

        ↓

Modelo empírico
(almacena todos los datos)

        ↓

Modelo paramétrico
(conserva únicamente unos pocos parámetros)

        ↓

Compresión de información
```

Llegamos así a una idea muy importante. Un modelo paramétrico no intenta recordar cada observación. Intenta descubrir la estructura que dio origen a las observaciones. 

Esta diferencia será fundamental durante el resto del curso. Cuando estudiemos redes neuronales veremos que, aunque sus millones de parámetros parezcan muy distintos de las distribuciones estadísticas clásicas, siguen persiguiendo exactamente el mismo objetivo. Construir una representación compacta capaz de explicar una enorme cantidad de datos. En la siguiente sección profundizaremos precisamente en esta idea y veremos que aprender puede interpretarse como un proceso de **compresión de información**, donde el verdadero desafío consiste en conservar únicamente aquello que resulta esencial para describir la realidad.

---

## Compresión de información

En las secciones anteriores estudiamos dos formas distintas de construir un modelo. Los modelos empíricos describen directamente las observaciones. Los modelos paramétricos, por el contrario, intentan resumir el comportamiento de los datos mediante un pequeño conjunto de parámetros. 

Ahora surge una pregunta aún más profunda.

> **¿Por qué los modelos paramétricos funcionan?**

Después de todo, ¿cómo es posible reemplazar miles o incluso millones de observaciones por únicamente unos pocos números? La respuesta proviene de una idea que aparece continuamente en Matemáticas, Física, Biología, Informática y, especialmente, en la teoría de la información.

La idea es sorprendentemente sencilla.

> **Aprender consiste en descubrir regularidades.**

Cuando encontramos una regularidad, dejamos de almacenar cada observación individual y comenzamos a almacenar únicamente la regla que las explica. En otras palabras,

> **aprender puede interpretarse como un proceso de compresión de información.**

---

## ¿Qué significa comprimir información?

Todos utilizamos mecanismos de compresión casi todos los días. Cuando tomamos una fotografía con un teléfono móvil, la imagen original contiene millones de píxeles. Sin embargo, normalmente no se almacena exactamente como fue capturada por el sensor. Antes de guardarse, la imagen se comprime utilizando formatos como JPEG. Durante ese proceso se elimina parte de la información. Los detalles menos importantes desaparecen. Las regiones muy similares se representan de forma mucho más eficiente. Como resultado, el archivo ocupa mucho menos espacio.

A pesar de ello, al observar la imagen resulta difícil notar diferencias importantes respecto a la fotografía original. La información no desapareció completamente. Fue reorganizada de una manera más eficiente.

---

### Un ejemplo cotidiano

Supongamos que una persona intenta memorizar el siguiente número.

```text
31415926535897932384626433832795
```

Probablemente necesite repetir la secuencia muchas veces.

Ahora imaginemos otra situación. La persona descubre que dicho número corresponde a los primeros dígitos del número

$$
\pi.
$$

En lugar de memorizar treinta cifras individuales, basta recordar una única idea:

> "Es el número π."

Toda la información queda representada mediante un concepto mucho más compacto. No recordamos cada dato. Recordamos la estructura que los genera. Aprender funciona exactamente de la misma manera.

---

## Los patrones contienen información

Consideremos la siguiente secuencia.

```text
3
6
9
12
15
18
21
24
```

Podemos almacenarla completa. O podemos observar un patrón. Cada número aumenta tres unidades respecto al anterior. Entonces basta escribir 

$$
x_n=3n.
$$

Una ecuación muy sencilla reemplaza una larga lista de observaciones. El patrón contiene la información esencial. Todo lo demás puede reconstruirse. Este ejemplo ilustra una idea muy importante.

> **Los modelos son mecanismos para descubrir patrones.**

Y una vez descubierto el patrón, ya no es necesario almacenar todos los datos originales.

---

## El papel de la redundancia

¿Por qué es posible comprimir información?

Porque los datos reales contienen redundancia. La redundancia aparece cuando cierta información puede deducirse a partir de otra.

Por ejemplo, si registramos la temperatura de una ciudad cada minuto, dos mediciones consecutivas suelen ser muy parecidas. Conocer una de ellas proporciona mucha información acerca de la siguiente. Existe una fuerte dependencia entre ambas.

Lo mismo ocurre en una fotografía. Los píxeles vecinos normalmente poseen colores muy similares. 

También ocurre en un texto. Después de la letra

```text
q
```

es muy probable encontrar la letra

```text
u.
```

La redundancia permite describir grandes cantidades de información mediante reglas mucho más sencillas.

---

## Aprender es descubrir regularidades

Podemos interpretar el aprendizaje desde una perspectiva completamente diferente. Un algoritmo recibe inicialmente una enorme cantidad de datos aparentemente desordenados. Su objetivo consiste en descubrir qué parte de esos datos corresponde a regularidades y qué parte corresponde simplemente a variaciones aleatorias. Una vez identificadas las regularidades, el modelo almacena únicamente dichas relaciones. Todo aquello que no puede explicarse mediante patrones permanecerá como incertidumbre.

Esta idea resulta extraordinariamente importante.

> **Un modelo no memoriza los datos; memoriza las regularidades presentes en los datos.**

---

## Una visión desde la Estadística

Podemos ilustrar esta idea mediante un ejemplo muy sencillo.

Supongamos que registramos durante un año la temperatura diaria de una ciudad. Observamos una gráfica como la siguiente.

```text
Temperatura

30 ───────────╮
              │╲
25 ─────────╮ │ ╲
            │ │  ╲
20 ───────╮ │ │   ╲
          │ │ │    ╲
15 ───────╯ ╰─╯─────╯──────── Tiempo
```

A simple vista observamos dos comportamientos diferentes. Existe una tendencia general asociada a las estaciones del año. Pero también aparecen pequeñas fluctuaciones diarias. Podemos interpretar la señal como

$$
Datos
=
Patrón
+
Ruido.
$$

El modelo intenta aprender únicamente el patrón. Las fluctuaciones aleatorias permanecerán como incertidumbre residual.

---

## El modelo como una explicación

Hasta este momento podríamos pensar que un modelo simplemente resume información.

Sin embargo, hace algo mucho más interesante. Intenta explicar por qué los datos presentan determinada estructura. 

Por ejemplo, si observamos que la altura de una planta aumenta casi linealmente durante cierto intervalo de tiempo, podemos construir una recta. La recta no almacena cada medición. Describe el mecanismo general del crecimiento. Algo similar ocurre con una distribución Normal. No memoriza todas las observaciones. Resume la tendencia central y la variabilidad del fenómeno. El conocimiento ya no está contenido en los datos. Está contenido en la estructura que los explica.

---

## El equilibrio entre simplicidad y precisión

Aquí aparece uno de los principios más importantes de toda la modelación.

Podríamos construir un modelo extremadamente complejo capaz de reproducir exactamente cada observación. Pero también podríamos construir un modelo excesivamente simple que ignore gran parte de la información. Ninguna de las dos opciones resulta deseable. Necesitamos encontrar un equilibrio. El modelo debe ser lo suficientemente simple para resumir los datos, pero también lo suficientemente preciso para describir correctamente el fenómeno.

Esta idea aparecerá nuevamente cuando estudiemos el sobreajuste (*overfitting*) y la generalización.

---

## El principio de parsimonia

En Ciencia existe un principio muy antiguo conocido como **principio de parsimonia** o **Navaja de Occam**. Puede resumirse de la siguiente manera.

> Entre dos modelos capaces de explicar igualmente bien un fenómeno, debe preferirse el más simple.

Esta idea no significa que los modelos simples siempre sean mejores Significa algo diferente. La complejidad únicamente debe incrementarse cuando los datos realmente lo justifican. Agregar parámetros innecesarios produce modelos más difíciles de interpretar y más propensos a aprender detalles accidentales de la muestra. Durante el resto del curso veremos que muchas técnicas modernas de aprendizaje automático pueden interpretarse precisamente como mecanismos para controlar esa complejidad.

---

## Información y capacidad de representación

Podemos imaginar ahora que cada parámetro representa una cierta capacidad para almacenar información acerca del fenómeno. Un modelo con pocos parámetros posee una capacidad limitada. Solo puede describir patrones muy sencillos. Un modelo con muchos parámetros puede representar relaciones mucho más complejas.

Sin embargo, una mayor capacidad no implica necesariamente un mejor aprendizaje. Si la capacidad supera ampliamente la información contenida en los datos, el modelo comenzará a memorizar detalles accidentales en lugar de descubrir regularidades. Esta observación será fundamental cuando estudiemos el compromiso entre **bias** y **varianza**.

---

## Una primera interpretación del aprendizaje

Podemos resumir todo lo visto hasta ahora mediante el siguiente esquema.

```text
Realidad

        ↓

Observaciones

        ↓

Regularidades + Variaciones aleatorias

        ↓

Modelo

        ↓

Representación compacta

        ↓

Predicción
```

Este diagrama resume gran parte del aprendizaje estadístico. Los datos contienen simultáneamente información útil y variaciones aleatorias. El modelo intenta separar ambas componentes. Las regularidades se convierten en conocimiento. Las variaciones no explicadas permanecen como incertidumbre.

---

## Mirando hacia adelante

En las secciones anteriores aprendimos que construir un modelo implica simplificar la realidad. También vimos que esa simplificación puede interpretarse como un proceso de compresión de información.
 
Sin embargo, todavía no sabemos cómo evaluar si dicha compresión fue buena o mala. Necesitamos una forma de responder preguntas como:

* ¿Qué tan diferente es nuestro modelo respecto a la realidad?

* ¿Cuánta información perdimos durante la compresión?

* ¿Cómo medir objetivamente la calidad de un modelo?

Responder estas preguntas requerirá introducir nuevas herramientas provenientes de la teoría de la información. Antes de llegar a ellas, estudiaremos un aspecto igualmente importante. Aunque un modelo sea correcto y esté perfectamente ajustado, existen varias fuentes de error que nunca desaparecen. Comprender el origen de esos errores será el siguiente paso en nuestro camino hacia una teoría completa del aprendizaje estadístico.

---

# Parte 2 — Las fuentes del error

## Error de muestreo

En la primera parte de esta unidad comprendimos que aprender consiste en construir un modelo a partir de una cantidad limitada de información. También vimos que un modelo puede interpretarse como una representación comprimida de la realidad.

Sin embargo, antes incluso de preocuparnos por la calidad del modelo, aparece una limitación mucho más profunda.

> **Nunca aprendemos directamente de la realidad. Aprendemos únicamente de una muestra de ella.**

Esta diferencia, que puede parecer sutil, constituye una de las principales fuentes de incertidumbre en Estadística y en Aprendizaje Automático. En esta sección estudiaremos por qué aparece este problema, cuál es su origen y cómo afecta cualquier proceso de aprendizaje.

---

### La realidad nunca está completamente disponible

Imaginemos que una empresa desea conocer la estatura promedio de todos sus clientes.

* La solución ideal sería sencilla.
* Bastaría medir absolutamente a todos.
* Obtendríamos entonces el valor exacto.
* Pero inmediatamente aparece una dificultad.
* Quizá la empresa tenga millones de clientes.
* Algunos ya no viven en la ciudad.
* Otros nunca responderán la encuesta.
* Nuevos clientes aparecen diariamente.
* La población cambia continuamente.
* En consecuencia, la población completa nunca está completamente disponible.

Esta situación no es una excepción. Es la regla. En prácticamente todos los problemas reales ocurre exactamente lo mismo.

---

### Aprender a partir de fragmentos

Podemos imaginar la realidad como un enorme rompecabezas.

```text
□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□
□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□
□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□
□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□
□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□
```

Nuestro conjunto de datos corresponde únicamente a unas pocas piezas.

```text
□□□□□□□□■□□□□□□□□□□■□□□□□□□□□□
□□□□□□□□□□□□□□■□□□□□□□□□□□□□□□
□□□□■□□□□□□□□□□□□□□□□□□□□□□□
□□□□□□□□□□□□■□□□□□□□□□□□□□□□
□□□□□□□□□□□□□□□■□□□□□□□□□□□□
```

A partir de esas pocas piezas intentamos reconstruir la imagen completa.  Esto significa que aprender siempre implica extrapolar información. El modelo intenta descubrir cómo es el resto del rompecabezas utilizando únicamente una pequeña fracción de las piezas.

---

### La población

En Estadística llamamos **población** al conjunto completo de elementos sobre los cuales deseamos obtener conocimiento.

Dependiendo del problema, la población puede ser:

* Todos los habitantes de un país.
* Todos los pacientes con una enfermedad.
* Todas las imágenes que podrían tomarse de un objeto.
* Todos los mensajes de correo electrónico.
* Todas las transacciones financieras de un banco.

En algunos problemas la población es finita. En otros casos puede considerarse prácticamente infinita. Por ejemplo, si entrenamos un sistema para reconocer automóviles, la cantidad de posibles fotografías que pueden capturarse es prácticamente ilimitada.

Nunca podremos observarlas todas.

---

### La muestra

La muestra corresponde únicamente al conjunto de observaciones que realmente utilizamos para aprender.

Podemos representarlo de la siguiente forma.

```text
Población

● ● ● ● ● ● ● ● ● ● ● ● ● ● ● ● ● ● ● ● ●

                 ↓

          Selección de datos

                 ↓

Muestra

● ● ● ● ● ● ● ● ● ●
```

Toda la información utilizada durante el entrenamiento proviene exclusivamente de la muestra. La población permanece oculta. Esta simple observación tiene consecuencias enormes.

---

#### Un ejemplo sencillo

Supongamos que deseamos estimar la estatura promedio de una universidad.

La población contiene 20 000 estudiantes. Seleccionamos aleatoriamente una muestra de 100 estudiantes.

Calculamos entonces

$$
\bar{x}=171.3\text{ cm}.
$$

¿Significa esto que el promedio real de toda la universidad es exactamente

171.3 cm?

No.

Significa únicamente que esa fue la media obtenida en nuestra muestra. Si hubiéramos seleccionado otros 100 estudiantes, probablemente habríamos obtenido un resultado ligeramente diferente.

---

### Muchas muestras posibles

Esta idea es extremadamente importante. La muestra que observamos no es la única posible. Podemos imaginar miles de muestras diferentes extraídas de la misma población.

```text
Población

● ● ● ● ● ● ● ● ● ● ● ● ● ● ● ● ●

        ↓

Muestra A

● ● ● ● ●

Media = 170.8

----------------------------

Muestra B

● ● ● ● ●

Media = 171.9

----------------------------

Muestra C

● ● ● ● ●

Media = 170.2

----------------------------

Muestra D

● ● ● ● ●

Media = 171.5
```

Todas las muestras provienen exactamente de la misma población. Sin embargo, producen resultados ligeramente diferentes. Esta variabilidad aparece únicamente porque observamos un subconjunto de la realidad.

---

### El origen del error de muestreo

Podemos definir ahora el concepto central de esta sección.

> **El error de muestreo es la diferencia entre las características de la muestra y las características reales de la población.**

No aparece porque el algoritmo esté equivocado. No aparece porque el modelo sea malo. Aparece simplemente porque observamos una cantidad limitada de información. Es un error inevitable. Incluso utilizando el mejor algoritmo del mundo seguirá existiendo.

---

#### Un ejemplo extremo

Imaginemos que lanzamos una moneda perfectamente balanceada.

Sabemos que

$$
P(\text{cara})=0.5.
$$

Ahora realizamos únicamente cuatro lanzamientos.

Podríamos obtener

```text
Cara
Cara
Cara
Cara
```

La distribución empírica sería

$$
\hat P(\text{cara})=1.
$$

Claramente este resultado no representa la verdadera probabilidad. No existe ningún error en el procedimiento. Simplemente tuvimos muy poca información. Si repetimos el experimento con 1000 lanzamientos, la frecuencia observada probablemente será mucho más cercana a

0.5.

---

### La Ley de los Grandes Números

Este fenómeno está relacionado con uno de los resultados más importantes de la Probabilidad.

La **Ley de los Grandes Números** establece que, a medida que aumenta el tamaño de la muestra, las frecuencias observadas tienden a aproximarse a las probabilidades verdaderas.

En términos sencillos, más datos producen estimaciones más estables.Podemos representarlo intuitivamente.

```text
Tamaño de muestra

10

      Error grande

----------------------------

100

    Error moderado

----------------------------

1000

 Error pequeño

----------------------------

100000

Error muy pequeño
```

Esto no significa que el error desaparezca completamente. Significa únicamente que, en promedio, disminuye conforme aumenta la cantidad de observaciones.

---

### Precisión e incertidumbre

Ahora podemos comprender una idea importante. Supongamos dos estudios.

Primer estudio:

100 observaciones.

Segundo estudio:

100 000 observaciones.

Ambos utilizan exactamente el mismo algoritmo.

El segundo estudio no necesariamente posee un modelo mejor. Lo que posee es una estimación mucho más estable. La diferencia proviene de la cantidad de evidencia disponible. En consecuencia, la incertidumbre asociada al modelo depende no solo del algoritmo utilizado, sino también de la cantidad de datos observados.

---

### Una interpretación probabilística

Podemos representar esta situación de manera muy sencilla. Existe una distribución verdadera, que llamaremos

$$
P(x).
$$

Sin embargo, nosotros únicamente observamos una distribución empírica, que escribiremos como

$$
\hat P(x).
$$

Nuestro objetivo consiste en que ambas sean lo más parecidas posible.

```text
Distribución verdadera

P(x)

        ↓

Muestreo

        ↓

Distribución empírica

P̂(x)
```

La diferencia entre ambas constituye precisamente el error de muestreo. Más adelante veremos que la divergencia de Kullback-Leibler permitirá cuantificar esta diferencia.

---

### Muestreo sesgado

Hasta ahora hemos supuesto que la muestra fue seleccionada aleatoriamente. Sin embargo, este supuesto no siempre se cumple. Supongamos que deseamos conocer la estatura promedio de toda una universidad. Si seleccionamos únicamente estudiantes del equipo de baloncesto, obtendremos un promedio considerablemente mayor que el real. 

El problema ya no es únicamente el tamaño de la muestra. La muestra dejó de ser representativa. Este fenómeno recibe el nombre de **sesgo de muestreo**. Los algoritmos no pueden corregir información que nunca observaron. Si los datos presentan sesgos importantes, el modelo inevitablemente aprenderá dichos sesgos. 

En aprendizaje automático suele decirse:

> **Un modelo es tan bueno como los datos con los que fue entrenado.**

---

### Más datos no siempre significan mejores datos

Una idea muy extendida consiste en pensar que basta con aumentar el tamaño de la base de datos para resolver todos los problemas. Sin embargo, esto no siempre es cierto. Imaginemos dos conjuntos de datos.

Primer conjunto:

1000 observaciones cuidadosamente seleccionadas de forma aleatoria.

Segundo conjunto:

un millón de observaciones obtenidas únicamente de una pequeña región del país.

Aunque el segundo conjunto sea mucho mayor, podría representar mucho peor la población completa. La calidad del muestreo resulta tan importante como la cantidad de datos.

---

### Error de muestreo y aprendizaje automático

Todo algoritmo de aprendizaje automático enfrenta exactamente el mismo problema. Durante el entrenamiento observa únicamente una muestra. Nunca conoce la distribución completa de los datos que encontrará en el futuro. Cuando posteriormente recibe nuevas observaciones, esperamos que sea capaz de responder correctamente. Esta capacidad dependerá, en gran medida, de qué tan representativa haya sido la muestra utilizada durante el entrenamiento.

En otras palabras, la calidad del aprendizaje comienza mucho antes del algoritmo. Comienza en la forma en que se obtuvieron los datos.

---

### Una primera conclusión

Podemos resumir esta sección mediante la siguiente idea.

```text
Realidad

        ↓

Población

        ↓

Muestreo

        ↓

Muestra

        ↓

Modelo
```

Cada flecha representa una pérdida potencial de información. El algoritmo nunca trabaja directamente con la realidad. Trabaja únicamente con la evidencia disponible. Por esta razón, todo modelo contiene inevitablemente cierta incertidumbre asociada al proceso de muestreo. 

En la siguiente sección descubriremos que este no es el único origen del error. Incluso si dispusiéramos de una muestra perfecta, el modelo todavía podría equivocarse. La causa ya no sería la falta de datos. La causa sería una representación inadecuada del fenómeno. Ese nuevo tipo de error recibe el nombre de **error estructural**.

---

## Error estructural

En la sección anterior descubrimos que todo proceso de aprendizaje comienza con una limitación inevitable: nunca observamos la población completa, sino únicamente una muestra.

Este hecho introduce el **error de muestreo**, una fuente de incertidumbre que disminuye cuando disponemos de datos más numerosos y representativos. Sin embargo, ahora imaginemos un escenario completamente diferente. Supongamos que, de alguna manera, logramos observar absolutamente todos los datos posibles.

Ya no existe error de muestreo. La población completa está disponible. Podríamos pensar que ahora nuestro modelo describirá perfectamente la realidad. Sorprendentemente, esto tampoco es cierto. Aparece entonces una segunda fuente de error, mucho más profunda.

> **Un modelo puede estar equivocado simplemente porque pertenece a la familia de modelos incorrecta.**

Este tipo de error recibe el nombre de **error estructural**.

---

### Un experimento mental

Supongamos que deseamos describir la trayectoria de una pelota lanzada al aire.

Observamos miles de mediciones muy precisas. La población completa está disponible. No existe ruido. No existe incertidumbre de medición. Todo parece perfecto.

Sin embargo, decidimos ajustar una recta.

```text
Altura

|
|          ●
|       ●
|     ●
|   ●
| ●
|________________________ Tiempo

Modelo:
──────────────
```

La realidad sigue una parábola.

Nosotros insistimos en utilizar una recta.

Aunque dispongamos de millones de observaciones, la recta nunca podrá representar correctamente el fenómeno. El problema ya no está en los datos. El problema está en el propio modelo.

---

### El modelo limita lo que podemos aprender

Esta idea resulta extraordinariamente importante. Todo algoritmo aprende únicamente dentro de la familia de modelos que se le permite utilizar.

Por ejemplo,

si elegimos una recta,

el algoritmo únicamente puede modificar:

* la pendiente,
* el intercepto.

Nada más. Nunca podrá producir una parábola. Nunca podrá producir una función sinusoidal. Nunca podrá producir una exponencial. La estructura del modelo limita aquello que puede aprender.

En otras palabras,

> **el algoritmo no puede descubrir relaciones que su modelo es incapaz de representar.**

---

#### Una analogía sencilla

Imaginemos que intentamos dibujar un círculo utilizando únicamente segmentos rectos.

Podemos aumentar el número de segmentos. Podemos hacerlos cada vez más pequeños. El dibujo mejorará progresivamente. Pero mientras estemos limitados a segmentos rectos, nunca obtendremos un círculo perfecto.

La limitación no proviene de nuestra habilidad para dibujar.

Proviene de la herramienta que elegimos. En modelación ocurre exactamente lo mismo. Los datos pueden ser excelentes. El algoritmo puede estar perfectamente implementado. Pero si la familia de modelos resulta insuficiente, siempre aparecerá un error inevitable.

---

### La familia de modelos

En la sección anterior hablamos del espacio de modelos.

Recordemos esa idea. Cuando seleccionamos una distribución Normal, no estamos eligiendo un único modelo. Estamos permitiendo que el algoritmo busque cualquier distribución Normal. Cuando utilizamos una regresión lineal, el algoritmo puede construir cualquier recta. Cuando utilizamos una regresión cuadrática, el algoritmo puede construir cualquier parábola.

Cada técnica define un conjunto diferente de funciones posibles. Podemos representar esta idea de la siguiente manera.

```text
Todos los fenómenos posibles

□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□

Familia de modelos elegida

┌─────────────────────────────┐
│                             │
│     Modelos posibles        │
│                             │
└─────────────────────────────┘

Realidad

                ★
```

Si la realidad se encuentra dentro de la familia elegida, el aprendizaje tiene posibilidades de encontrarla.

Si no pertenece a dicha familia, ningún algoritmo podrá reconstruirla exactamente.

---

#### Un ejemplo estadístico

Supongamos que registramos el número de llamadas que recibe un centro de atención cada minuto. Observamos una distribución claramente asimétrica. Sin embargo, decidimos modelarla mediante una distribución Normal. Podemos calcular cuidadosamente

$$
\mu
$$

y

$$
\sigma.
$$

Incluso podemos utilizar millones de observaciones. A pesar de ello, las colas de la distribución seguirán estando mal representadas. La razón es sencilla. La distribución Normal supone simetría. Los datos reales no la poseen. El problema no aparece porque la media esté mal calculada. Aparece porque elegimos una familia de modelos inadecuada.

---

### Aprender dentro de una familia

Podemos representar el proceso de aprendizaje de la siguiente forma.

```text
Realidad

        ↓

Elegimos una familia de modelos

        ↓

El algoritmo busca el mejor modelo
dentro de esa familia

        ↓

Modelo aprendido
```

Esta representación aclara una idea muy importante. El algoritmo no busca cualquier modelo imaginable. Busca únicamente entre aquellos que nosotros le permitimos utilizar.

---

### El mejor modelo posible... dentro de sus limitaciones

Supongamos nuevamente que ajustamos una recta a una parábola. El algoritmo encontrará la mejor recta posible. No cometerá errores matemáticos. No fallará durante la optimización. Simplemente encontrará la recta que minimiza el error. Pero seguirá siendo una recta.

Esta observación permite comprender otra idea muy utilizada en aprendizaje automático.

> **El mejor modelo disponible no siempre es un buen modelo.**

Puede ser únicamente el mejor dentro de una familia insuficiente.

---

### La capacidad de representación

A medida que estudiamos distintos algoritmos aparece un nuevo concepto.

La **capacidad de representación**.

La capacidad representa la diversidad de funciones que un modelo puede construir.

Por ejemplo, una recta posee poca capacidad. Solo puede representar relaciones lineales.

Una parábola posee una capacidad ligeramente mayor. Un polinomio de grado diez puede representar formas mucho más complejas. Una red neuronal profunda puede aproximar relaciones extremadamente complicadas.

Podemos imaginar una escala.

```text
Capacidad de representación

Recta
│
├───────────────┐
│               │
Parábola        │
│               │
├────────────────────────────┐
│                            │
Polinomios                   │
│                            │
├───────────────────────────────────────────────┐
│                                               │
Red neuronal profunda                           │
```

A medida que aumenta la capacidad, el modelo puede representar fenómenos cada vez más complejos.

Sin embargo, como veremos más adelante, una mayor capacidad también introduce nuevos riesgos.

---

### Error estructural y capacidad

Ahora podemos conectar ambas ideas.

Si la capacidad del modelo resulta demasiado pequeña, ciertas relaciones nunca podrán representarse. Aparecerá entonces un error permanente. No importa cuántos datos observemos. No importa cuánto tiempo entrenemos el algoritmo. El error permanecerá. Este comportamiento puede resumirse mediante la siguiente idea.

```text
Capacidad insuficiente

↓

Relaciones imposibles de representar

↓

Error estructural
```

---

#### Un ejemplo en reconocimiento de imágenes

Imaginemos que deseamos construir un sistema para reconocer rostros.

Nuestro modelo únicamente utiliza dos variables:

* altura de la imagen,
* ancho de la imagen.

Claramente esta información resulta insuficiente. Dos fotografías completamente distintas pueden tener exactamente el mismo tamaño. Aunque dispongamos de millones de imágenes, el modelo seguirá fallando.

Las variables elegidas simplemente no contienen suficiente capacidad descriptiva.

En este caso, el error estructural no proviene únicamente del algoritmo. Proviene del propio diseño del modelo.

---

### La diferencia con el error de muestreo

Conviene detenernos un momento para comparar ambas fuentes de error.

#### Error de muestreo

La familia de modelos podría ser correcta.

Sin embargo, la muestra resulta insuficiente. Más datos ayudan.

---

#### Error estructural

La muestra puede ser enorme.

Sin embargo,  la familia de modelos es incapaz de representar el fenómeno. Más datos ya no ayudan. Necesitamos cambiar el modelo.

Esta diferencia es fundamental. En muchos proyectos de ciencia de datos se intenta resolver todos los problemas recolectando más información.

Sin embargo, cuando el origen del error es estructural, ninguna cantidad de datos solucionará el problema. La única solución consiste en utilizar una familia de modelos más adecuada.

---

### El compromiso inevitable

Podríamos pensar entonces que basta con utilizar siempre el modelo más complejo posible.
 
Sin embargo, esto tampoco funciona.

Un modelo excesivamente complejo puede comenzar a memorizar detalles accidentales de la muestra en lugar de descubrir las regularidades del fenómeno.

Aparecerá entonces otro problema completamente diferente:

el **sobreajuste** (*overfitting*).

En consecuencia, el verdadero desafío del aprendizaje estadístico consiste en encontrar un equilibrio. El modelo debe poseer suficiente capacidad para representar el fenómeno, pero no tanta como para memorizar el ruido presente en los datos.

Esta idea aparecerá repetidamente durante el resto del curso.

---

### Una conclusión importante

Podemos resumir esta sección mediante el siguiente esquema.

```text
Realidad

        ↓

Familia de modelos elegida

        ↓

Capacidad de representación

        ↓

Modelo aprendido

        ↓

Error estructural
```

El error estructural no depende de la cantidad de datos.

Depende de la capacidad del modelo para representar el fenómeno. Comprender esta diferencia resulta esencial para interpretar correctamente cualquier proceso de aprendizaje. En la siguiente sección estudiaremos una tercera fuente de error aún más profunda.

Incluso si utilizamos una muestra perfecta y un modelo capaz de representar exactamente la realidad, seguirá existiendo una parte del fenómeno que ningún algoritmo podrá eliminar.

Dicha componente corresponde a la **aleatoriedad inherente del proceso** y da origen a la incertidumbre residual.

---

## Aleatoriedad e incertidumbre residual

En las dos secciones anteriores descubrimos que un modelo puede equivocarse por dos razones diferentes.

La primera aparece porque nunca observamos la población completa. Este fenómeno dio origen al **error de muestreo**.

La segunda aparece porque el modelo elegido puede ser incapaz de representar correctamente el fenómeno. Esta limitación dio origen al **error estructural**.

Podríamos pensar entonces que, si resolvemos ambos problemas, obtendremos un modelo perfecto.

Imaginemos el escenario ideal. Disponemos de toda la población. El modelo pertenece exactamente a la familia correcta. No existen errores de programación. No existen aproximaciones numéricas.

¿Significa esto que ahora podremos predecir perfectamente el futuro?

La respuesta, sorprendentemente, sigue siendo **no**.

Existe una tercera fuente de incertidumbre que no depende ni de los datos ni del modelo. Depende del propio fenómeno que estamos intentando describir.

Esta componente recibe el nombre de **aleatoriedad** o **incertidumbre residual**.

---

### Cuando la naturaleza es impredecible

Imaginemos que lanzamos una moneda perfectamente balanceada. Conocemos exactamente su probabilidad de producir cara. Sabemos que

$$
P(\text{cara})=0.5.
$$

Supongamos incluso que conocemos perfectamente las leyes de la probabilidad.

¿Podemos predecir el resultado del siguiente lanzamiento? No.

Podemos conocer perfectamente la distribución del fenómeno. Pero no el resultado de una observación individual.

Esto constituye una diferencia fundamental.

> **Conocer las probabilidades no implica conocer el resultado de cada evento.**

---

### Predicción individual y comportamiento colectivo

Este fenómeno aparece continuamente en Estadística.

Por ejemplo, nadie puede predecir exactamente el momento en que una persona llegará al servicio de urgencias de un hospital.

Sin embargo, sí es posible estimar cuántos pacientes llegarán, en promedio, durante una hora.

De manera similar, no podemos predecir cuál gota específica caerá primero durante una lluvia. Pero sí podemos estimar la cantidad total de lluvia que caerá durante el día.

En consecuencia, muchos fenómenos son impredecibles a nivel individual, pero extraordinariamente predecibles cuando observamos grandes conjuntos de eventos.

---

### Una fuente diferente de incertidumbre

Conviene comparar nuevamente las tres fuentes de error que hemos estudiado hasta ahora.

#### Error de muestreo

No observamos toda la población. Más datos ayudan.

---

#### Error estructural

Elegimos una familia de modelos inadecuada. Un mejor modelo ayuda.

---

#### Incertidumbre residual

El propio fenómeno contiene una componente aleatoria. Ni más datos ni un modelo más complejo pueden eliminarla completamente. Esta tercera fuente de incertidumbre representa un límite fundamental del conocimiento.

---

### Un ejemplo en Medicina

Supongamos que deseamos predecir la presión arterial de un paciente.

Disponemos de información muy completa.

Conocemos:

* edad,
* peso,
* estatura,
* antecedentes familiares,
* alimentación,
* actividad física,
* medicamentos,
* enfermedades previas.

Incluso podríamos incorporar cientos de variables adicionales.

A pesar de ello, si medimos la presión arterial dos veces con pocos minutos de diferencia, bbtendremos valores ligeramente distintos.

¿Por qué?

Porque existen innumerables factores imposibles de controlar completamente.

El organismo cambia continuamente. La respiración cambia. El nivel de estrés cambia. La posición corporal cambia. Incluso la precisión del instrumento introduce pequeñas variaciones.

En consecuencia, siempre permanecerá una parte impredecible del fenómeno.

---

### El ruido

En muchos problemas esta componente aleatoria recibe el nombre de **ruido**.

Podemos representar una observación mediante la expresión

$$
Y
=
f^\star(X)
+
\varepsilon
$$

donde

* $f^\star(X)$ representa la relación verdadera entre las variables.

* $\varepsilon$ representa todas aquellas variaciones que el modelo no puede explicar.

Este término puede incluir muchas causas diferentes.

Por ejemplo,

* errores de medición,
* fluctuaciones naturales,
* variables no observadas,
* efectos ambientales,
* procesos inherentemente aleatorios.

El símbolo

$$
\varepsilon
$$

resume toda la incertidumbre que permanece incluso cuando conocemos perfectamente el modelo.

---

### Una interpretación gráfica

Podemos imaginar una nube de datos como la siguiente.

```text
Y

│                    •
│               •
│           •
│      •
│   •
│ •
└────────────────────────── X
```

Podemos observar una tendencia general.

Sin embargo, ningún conjunto de puntos cae exactamente sobre una única curva. Siempre existe cierta dispersión alrededor del comportamiento promedio. La curva representa el conocimiento del modelo. La dispersión representa la incertidumbre residual.

---

### ¿Qué parte puede aprender un algoritmo?

Esta pregunta resulta fundamental.

Supongamos nuevamente la ecuación

$$
Y
=
f^\star(X)
+
\varepsilon.
$$

El algoritmo únicamente puede aprender

$$
f^\star(X).
$$

Nunca podrá aprender

$$
\varepsilon.
$$

¿Por qué?

Porque el ruido no sigue un patrón estable. Si existiera un patrón, dejaría de ser ruido. Pasaría a formar parte del modelo. Esta observación permite comprender una idea muy importante.

> **El aprendizaje consiste precisamente en separar el patrón del ruido.**

---

### El peligro de aprender el ruido

Aquí aparece uno de los problemas más importantes del aprendizaje automático. Supongamos que nuestro modelo posee una enorme capacidad. Podría intentar explicar incluso pequeñas fluctuaciones aleatorias de la muestra. A primera vista parecería un excelente resultado. El error sobre los datos de entrenamiento sería muy pequeño. Sin embargo, esas pequeñas variaciones no corresponden al fenómeno. Corresponden únicamente al ruido presente durante la medición. Cuando el modelo memoriza ese ruido, pierde capacidad para generalizar.

Este fenómeno será estudiado posteriormente bajo el nombre de **sobreajuste** (*overfitting*).

---

### El límite del aprendizaje

Existe una consecuencia muy interesante. Podemos mejorar continuamente nuestros algoritmos. Podemos utilizar modelos más sofisticados. Podemos recolectar millones de observaciones adicionales. Podemos construir computadores cada vez más rápidos. Sin embargo, ninguna de estas mejoras podrá eliminar completamente la incertidumbre residual. Existe un límite impuesto por la propia naturaleza del fenómeno. Este límite no depende de la tecnología. Depende del comportamiento del mundo real.

---

#### Una analogía sencilla

Imaginemos que observamos un río.

* Podemos describir muy bien su recorrido.
* Podemos calcular su velocidad promedio.
* Podemos estimar el caudal.

Sin embargo, si observamos cuidadosamente la superficie del agua, descubriremos pequeñas ondulaciones producidas por el viento. Intentar predecir exactamente la posición de cada una de esas pequeñas ondas resulta prácticamente imposible. No porque nuestro modelo sea malo. Sino porque el sistema contiene una enorme cantidad de pequeñas perturbaciones imposibles de controlar. El aprendizaje automático enfrenta continuamente situaciones similares. El modelo describe la corriente principal. Las pequeñas ondulaciones permanecen como incertidumbre.

---

## Las tres fuentes del error

Ahora podemos reunir todas las ideas desarrolladas hasta este punto.

```text
Realidad

        │

        ├───────────────► Error de muestreo
        │
        │   Observamos únicamente una muestra.

        ▼

Modelo elegido

        │

        ├───────────────► Error estructural
        │
        │   El modelo puede ser insuficiente.

        ▼

Fenómeno real

        │

        ├───────────────► Incertidumbre residual
        │
        │   Parte del fenómeno permanece aleatoria.

        ▼

Predicción
```

Estas tres componentes aparecen prácticamente en cualquier problema de aprendizaje estadístico. Comprenderlas constituye el primer paso para interpretar correctamente el comportamiento de cualquier algoritmo.

Miremos esta descripción de los errores en este libro [Explicación fuentes de error](fuentes_de_error.ipynb)

---

### Una primera descomposición del error

Podemos resumir la discusión anterior mediante una expresión conceptual.

```text
Error total

=

Error de muestreo

+

Error estructural

+

Incertidumbre residual
```

Esta expresión no pretende ser todavía una igualdad matemática exacta. Su propósito consiste en mostrar que el error observado puede tener diferentes orígenes. Dependiendo del problema, una de estas componentes puede dominar sobre las demás. En algunos casos necesitaremos más datos. En otros deberemos cambiar completamente el modelo. Y en otros simplemente tendremos que aceptar que una parte del fenómeno nunca podrá predecirse con absoluta precisión.

---

### Una visión desde la teoría del conocimiento

Las tres fuentes de error pueden interpretarse también desde una perspectiva filosófica. Existe una parte de la realidad que desconocemos porque aún no la hemos observado. Existe otra parte que conocemos, pero que nuestros modelos no saben representar. Y finalmente existe una parte que, aun siendo observable, permanece inherentemente incierta. El aprendizaje consiste en reducir las dos primeras. La tercera constituye un límite natural del conocimiento. Esta idea aparece continuamente en Ciencia. No todo lo desconocido es desconocido por falta de información. En ocasiones lo desconocido forma parte de la propia naturaleza del fenómeno.

---

### Mirando hacia adelante

Hasta este momento hemos estudiado por qué los modelos se equivocan. Sin embargo, todavía no sabemos cómo cuantificar dichos errores. Necesitamos una forma objetiva de comparar un modelo con la realidad. Necesitamos medir cuánta información pierde un modelo. 

Necesitamos responder preguntas como:

* ¿Qué tan diferente es una distribución respecto a otra?
* ¿Cómo comparar dos modelos probabilísticos?
* ¿Cómo medir objetivamente la calidad de una aproximación?

La respuesta proviene nuevamente de la teoría de la información. En las siguientes secciones introduciremos la **divergencia de Kullback-Leibler**, una herramienta que permitirá medir la distancia informacional entre dos distribuciones de probabilidad y que servirá como fundamento para comprender posteriormente la entropía cruzada, la máxima verosimilitud y gran parte del aprendizaje profundo.

---

# Parte 3 — Midiendo la calidad de un modelo

## La divergencia de Kullback-Leibler (KL)

Hasta este momento hemos construido una idea bastante completa acerca del aprendizaje. Sabemos que un modelo intenta representar una realidad compleja utilizando una representación mucho más sencilla. También comprendimos que dicha representación nunca es perfecta. Puede equivocarse porque observamos únicamente una muestra. Puede equivocarse porque el modelo elegido es insuficiente. Y puede equivocarse porque el propio fenómeno contiene incertidumbre. 

Sin embargo, todavía no hemos respondido una pregunta fundamental. 

> **¿Cómo podemos medir qué tan bueno es un modelo?**

Responder esta pregunta constituye uno de los objetivos principales de la teoría de la información. Necesitamos una forma objetiva de comparar dos distribuciones de probabilidad. Necesitamos medir qué tan diferente es nuestro modelo respecto al fenómeno real. La herramienta que utilizaremos recibe el nombre de **divergencia de Kullback-Leibler**, o simplemente **divergencia KL**.

---

### Comparar distribuciones

Supongamos que disponemos de dos distribuciones de probabilidad. La primera representa el comportamiento real del fenómeno. La escribiremos como

$$
P(x).
$$

La segunda corresponde al modelo aprendido. La escribiremos como

$$
Q(x).
$$

Nuestro objetivo consiste en responder una pregunta muy sencilla.

> **¿Qué tan parecidas son ambas distribuciones?**

Si ambas son prácticamente iguales, diremos que el modelo representa correctamente la realidad. Si son muy diferentes, el modelo contiene una gran cantidad de error.

---

### Una primera intuición

Imaginemos dos mapas. Uno representa exactamente una ciudad. El otro contiene algunas calles desplazadas y otras completamente ausentes. Ambos intentan describir el mismo lugar. Sin embargo, claramente uno de ellos resulta mejor que el otro. Necesitamos alguna medida que cuantifique esa diferencia. Con las distribuciones ocurre exactamente lo mismo. Dos distribuciones pueden parecer similares a simple vista. Pero necesitamos una medida objetiva que permita responder cuánto difieren realmente.

---

### ¿Por qué no restar probabilidades?

Podría parecer suficiente calcular

$$
P(x)-Q(x).
$$

Sin embargo, esta idea presenta varios problemas.

Supongamos las siguientes distribuciones.

| Valor | P(x) | Q(x) |
|--------|------|------|
| A | 0.50 | 0.45 |
| B | 0.50 | 0.55 |

Las diferencias son

```text
0.05

-0.05
```

Si las sumamos obtenemos 0.

La conclusión sería absurda. Las distribuciones son diferentes, pero la suma de las diferencias vale cero. Necesitamos una medida más inteligente.

---

### La información asociada a un evento

Para construir esa medida recordemos una idea estudiada en unidades anteriores.

Cuando ocurre un evento con probabilidad

$$
P(x),
$$

la información asociada a dicho evento viene dada por

$$
I(x)
=
-\log P(x).
$$

Esta expresión refleja una idea muy intuitiva. Los eventos muy improbables producen mucha información. Los eventos muy frecuentes producen poca información. Por ejemplo, si todos los días sale el Sol, esa observación prácticamente no aporta información nueva. En cambio, si mañana el Sol no apareciera, la información obtenida sería enorme. La teoría de la información mide precisamente esta sorpresa. 

---

### Dos formas de describir la realidad

Supongamos ahora que el fenómeno real sigue la distribución

$$
P(x).
$$

Pero nosotros creemos que sigue

$$
Q(x).
$$

Cuando observamos un evento, el fenómeno genera información de acuerdo con

$$
P.
$$

Sin embargo, nuestro modelo calcula la información utilizando

$$
Q.
$$

Si ambas distribuciones fueran idénticas, ambas asignarían exactamente la misma cantidad de información. Pero si son diferentes, nuestro modelo describirá incorrectamente algunos eventos.

En consecuencia, necesitaremos más información para describir la realidad. Aquí aparece la idea central de la divergencia KL.

---

### Una interpretación desde la compresión

Recordemos la interpretación desarrollada en la sección anterior. Aprender consiste en construir una representación comprimida de la realidad. Imaginemos ahora que deseamos comprimir un archivo. Disponemos de dos algoritmos de compresión. El primero fue diseñado específicamente para ese tipo de información. El segundo fue construido suponiendo una estructura completamente diferente. ¿Cuál producirá archivos más pequeños?

Naturalmente, el primero. Porque comprende mejor la estructura de los datos. La divergencia KL puede interpretarse precisamente como la pérdida de eficiencia producida cuando utilizamos un modelo incorrecto para representar la realidad.

En otras palabras, mide cuánta información adicional necesitamos debido a que nuestro modelo no coincide exactamente con el fenómeno observado.

---

### Una analogía cotidiana

Supongamos que deseamos traducir un libro. Si conocemos perfectamente el idioma original, la traducción resultará sencilla. Pero imaginemos que creemos, equivocadamente, que el libro fue escrito en otro idioma. Cada frase comenzará a interpretarse incorrectamente. Necesitaremos realizar muchas más correcciones. El trabajo aumentará considerablemente. No porque el libro sea más difícil. Sino porque utilizamos un modelo equivocado para interpretarlo.

La divergencia KL mide exactamente ese costo adicional.

---

### La idea fundamental

Podemos resumir todo lo anterior mediante una única frase.

> **La divergencia KL mide cuánta información adicional necesitamos cuando describimos una distribución utilizando un modelo incorrecto.**

Esta interpretación resulta mucho más profunda que pensar simplemente en una distancia entre distribuciones. No estamos comparando únicamente números. Estamos comparando dos formas distintas de representar la realidad.

---

### Construyendo la divergencia

Ya conocemos dos ingredientes fundamentales. El primero corresponde a la información de un evento,

$$
-\log(P(x)).
$$

El segundo corresponde a las probabilidades verdaderas,

$$
P(x).
$$

La idea consiste en calcular la información promedio que perderíamos si utilizáramos

$$
Q(x)
$$

para describir eventos que realmente siguen

$$
P(x).
$$

La expresión resultante es

$$
D_{KL}(P\|Q)
=
\sum_x
P(x)
\log
\frac{P(x)}
{Q(x)}.
$$

No analizaremos todavía todos los detalles matemáticos de esta expresión. Por el momento nos interesa comprender su significado.

---

### Interpretación de la expresión

Observemos cuidadosamente la fórmula. Aparecen dos distribuciones diferentes. La primera,

$$
P(x),
$$

representa la realidad.

La segunda,

$$
Q(x),
$$

representa el modelo.

El cociente

$$
\frac{P(x)}{Q(x)}
$$

compara ambas probabilidades.

Si ambas coinciden,

el cociente vale uno.

Sabemos además que

$$
\log(1)=0.
$$

Por tanto,

cada evento cuya probabilidad esté correctamente representada no aporta divergencia. La divergencia aparece únicamente cuando ambas distribuciones comienzan a diferir. Esta observación resulta muy intuitiva. Si el modelo describe exactamente la realidad, no existe pérdida de información.

---

### ¿Qué significa un valor grande?

Supongamos que para cierto evento

la realidad asigna

$$
P(x)=0.40,
$$

mientras que nuestro modelo asigna

$$
Q(x)=0.01.
$$

El modelo considera ese evento extremadamente improbable, aunque en realidad ocurre con bastante frecuencia. Cada vez que dicho evento aparezca, el modelo cometerá una sorpresa mucho mayor de la esperada. Necesitaremos más información para describir el fenómeno. La divergencia KL aumentará.

En consecuencia, valores grandes de KL indican modelos que describen pobremente la realidad.

---

### ¿Qué significa un valor pequeño?

Ahora imaginemos que ambas distribuciones prácticamente coinciden.

```text
P(x)

██████████

Q(x)

█████████▉
```

Las diferencias son muy pequeñas. El modelo asigna probabilidades muy similares a las verdaderas. En este caso, la pérdida de información también será pequeña. La divergencia KL tomará un valor cercano a cero. Esto significa que el modelo constituye una buena aproximación del fenómeno.

---

### Una propiedad importante

La divergencia KL nunca es negativa.

Siempre se cumple que

$$
D_{KL}(P\|Q)
\ge
0.
$$

Además,

el valor cero únicamente aparece cuando ambas distribuciones coinciden exactamente. Esto resulta coherente con nuestra interpretación. Si el modelo representa perfectamente la realidad, no existe pérdida de información. Toda representación incorrecta introduce necesariamente un costo adicional.

---

### KL no es una distancia

Aunque muchas veces se habla informalmente de "distancia", la divergencia KL no constituye una distancia matemática.

¿Por qué?

Porque no cumple una propiedad muy importante. En general,

$$
D_{KL}(P\|Q)
\neq
D_{KL}(Q\|P).
$$

El orden importa. No es lo mismo medir cuánto pierde el modelo al representar la realidad, que cuánto perdería la realidad si intentara representar al modelo. Esta diferencia posee una interpretación muy clara. En aprendizaje automático, la distribución importante siempre es

$$
P(x),
$$

porque representa el fenómeno real. Nuestro objetivo consiste en aproximar

$$
P,
$$

no al contrario.

---

### Una nueva forma de entender el aprendizaje

Llegamos así a una interpretación completamente diferente del aprendizaje estadístico. Hasta ahora habíamos dicho que aprender consistía en construir un modelo. Ahora podemos expresarlo de otra manera. 

> **Aprender consiste en encontrar un modelo cuya divergencia KL respecto a la realidad sea lo más pequeña posible.**

Esta idea unifica gran parte de lo estudiado hasta ahora. Los modelos empíricos, los modelos paramétricos, Maximum Likelihood, la inferencia bayesiana, todos persiguen exactamente el mismo objetivo. Reducir la diferencia entre el modelo y el fenómeno real.

En las siguientes secciones veremos que esta misma idea reaparece bajo otros nombres. La entropía cruzada, la máxima verosimilitud e incluso las funciones de pérdida utilizadas para entrenar redes neuronales constituyen distintas formas de expresar exactamente este mismo principio.

---

### Propiedades e interpretación de la divergencia de Kullback-Leibler

En la sección anterior introdujimos la divergencia de Kullback-Leibler como una medida de la diferencia entre un modelo probabilístico y la realidad.

Más concretamente, vimos que si

* \(P(x)\) representa la distribución verdadera del fenómeno, y
* \(Q(x)\) representa nuestro modelo,

entonces la divergencia KL cuantifica la pérdida de información producida cuando utilizamos \(Q\) para describir eventos que realmente siguen \(P\).

Aunque esta definición resulta muy poderosa, todavía es bastante abstracta. En esta sección construiremos una intuición mucho más profunda acerca de esta medida. Nuestro objetivo no será memorizar una fórmula, sino comprender qué significa realmente un determinado valor de divergencia.

---

### Una primera interpretación

Imaginemos nuevamente que intentamos describir la realidad mediante un modelo. Si el modelo coincide exactamente con la realidad, no existe ninguna pérdida de información. Nuestro modelo "espera" exactamente los mismos eventos que realmente ocurren. Podemos representar esta situación de la siguiente forma.

```text
Realidad

████████████████

Modelo

████████████████
```

Ambas distribuciones coinciden. No existe información adicional que aprender. En consecuencia, la divergencia KL es igual a cero.

---

### Cuando el modelo comienza a equivocarse

Supongamos ahora que nuestro modelo asigna probabilidades ligeramente diferentes.

```text
Realidad

████████████████

Modelo

███████████▌████
```

Las diferencias son pequeñas. La mayoría de los eventos siguen recibiendo probabilidades similares. El modelo todavía representa razonablemente bien el fenómeno. La divergencia KL será pequeña. En este caso podemos interpretar el modelo como una buena aproximación.

---

### Cuando el modelo describe otro fenómeno

Ahora imaginemos una situación completamente distinta.

```text
Realidad

████████████████

Modelo

██▌████████
```

Muchas probabilidades son completamente diferentes.

El modelo espera eventos que casi nunca ocurren. Y asigna probabilidades muy pequeñas a eventos frecuentes. Cada nueva observación produce una gran sorpresa. La cantidad de información adicional necesaria aumenta considerablemente. En consecuencia, la divergencia KL toma valores mucho mayores.

---

#### Un ejemplo numérico

Supongamos la siguiente distribución verdadera.

| Resultado | P(x) |
|-----------|------|
| A | 0.70 |
| B | 0.20 |
| C | 0.10 |

Construimos ahora dos modelos.

Modelo 1

| Resultado | Q₁(x) |
|-----------|--------|
| A | 0.68 |
| B | 0.22 |
| C | 0.10 |

Modelo 2

| Resultado | Q₂(x) |
|-----------|--------|
| A | 0.20 |
| B | 0.30 |
| C | 0.50 |

A simple vista observamos que el primer modelo resulta mucho más parecido a la distribución verdadera. En consecuencia, esperamos que

$$
D_{KL}(P||Q_1)
<
D_{KL}(P||Q_2).
$$

Esta observación coincide exactamente con nuestra intuición. La divergencia KL aumenta cuando el modelo comienza a representar peor la realidad.

---

### ¿Qué ocurre evento por evento?

Una de las ventajas de la divergencia KL consiste en que permite analizar el aporte individual de cada evento. Supongamos que cierto evento ocurre con frecuencia elevada.

Por ejemplo,

$$
P(x)=0.60.
$$

Nuestro modelo, sin embargo, estima

$$
Q(x)=0.10.
$$

Cada vez que dicho evento ocurra, el modelo experimentará una enorme sorpresa. Como además ese evento ocurre con frecuencia, su contribución a la divergencia será considerable. Por el contrario, si un evento aparece muy raramente, su contribución también será pequeña, incluso cuando el modelo se equivoque ligeramente. Esto explica por qué la divergencia pondera las diferencias utilizando

$$
P(x).
$$

Los eventos importantes tienen mayor influencia.

---

### El significado de KL = 0

La propiedad más importante de la divergencia KL puede resumirse de manera muy sencilla.

Siempre se cumple

$$
D_{KL}(P||Q)\ge0.
$$

Y además,

$$
D_{KL}(P||Q)=0
$$

únicamente cuando

$$
P(x)=Q(x)
$$

para todos los valores posibles de

$$
x.
$$

Esta propiedad resulta perfectamente coherente con nuestra interpretación. Si el modelo representa exactamente la realidad, no existe pérdida de información. No necesitamos información adicional para describir el fenómeno.

---

### ¿Puede ser negativa?

Esta pregunta aparece con frecuencia cuando se estudia la divergencia KL por primera vez. La respuesta es no. Nunca obtendremos valores negativos. Aunque algunos términos individuales de la suma puedan ser negativos, el resultado total siempre será mayor o igual que cero.

Este resultado constituye uno de los teoremas fundamentales de la teoría de la información y recibe el nombre de **desigualdad de Gibbs**. Más adelante veremos que esta propiedad desempeña un papel esencial en la demostración de muchos algoritmos de aprendizaje.

---

### ¿Existe un valor máximo?

Curiosamente, la respuesta también es no. La divergencia KL no posee un límite superior. Supongamos que el fenómeno real asigna

$$
P(x)=0.30
$$

a un determinado evento, mientras que nuestro modelo considera prácticamente imposible dicho evento.

Es decir,

$$
Q(x)\approx0.
$$

Entonces

$$
\log\left(\frac{P(x)}{Q(x)}\right)
$$


crece rápidamente. La divergencia puede hacerse arbitrariamente grande. Esto refleja una idea intuitiva. Cuando un modelo considera imposible un evento que en realidad ocurre con frecuencia, su descripción del fenómeno resulta extremadamente deficiente.

---

### ¿Por qué el orden importa?

Recordemos una propiedad mencionada anteriormente.

En general,

$$
D_{KL}(P||Q)
\neq
D_{KL}(Q||P).
$$

Esta diferencia suele sorprender inicialmente. Sin embargo, posee una interpretación muy sencilla. Imaginemos dos mapas. Uno corresponde a la ciudad real. El otro contiene numerosos errores. Si deseamos medir cuánto se equivoca el mapa respecto a la ciudad, debemos utilizar la ciudad como referencia. Invertir el orden significa responder una pregunta completamente diferente. Con las distribuciones ocurre exactamente lo mismo. En aprendizaje automático, la realidad constituye siempre el punto de referencia.

Nuestro objetivo consiste en aproximar

$$
P,
$$

no modificar la realidad para parecerse al modelo.

---

### Una analogía con un idioma

Supongamos que deseamos escribir correctamente un texto en español. El idioma español posee ciertas probabilidades naturales. Después de la letra

```text
q
```

casi siempre aparece

```text
u
```

Imaginemos ahora que construimos un modelo del idioma donde esa regla prácticamente nunca ocurre. Cada vez que aparezca una palabra como

```text
que

quien

quizá
```

el modelo se sorprenderá.

Necesitará mucha más información para describir correctamente el texto. La divergencia KL cuantifica precisamente ese costo adicional. Mientras más se aleje el modelo de las verdaderas probabilidades del idioma, mayor será la pérdida de información.

---

### ¿Qué significa una divergencia pequeña?

Conviene responder esta pregunta con cuidado. Una divergencia pequeña no significa que el modelo sea perfecto. Significa únicamente que las probabilidades asignadas por el modelo son muy parecidas a las verdaderas. Todavía pueden existir diferencias. Sin embargo, desde el punto de vista informacional, el costo adicional producido por dichas diferencias resulta reducido.

En consecuencia, KL permite comparar objetivamente distintos modelos. Aquel cuya divergencia sea menor representa mejor el fenómeno observado.

---

### Una herramienta para comparar modelos

Supongamos que entrenamos tres modelos distintos utilizando exactamente los mismos datos.

Obtenemos

```text
Modelo A

KL = 0.31

------------------------

Modelo B

KL = 0.08

------------------------

Modelo C

KL = 0.56
```

Podemos concluir inmediatamente que el modelo B constituye la mejor aproximación de los tres. No porque produzca mayor precisión en una observación particular, sino porque, en promedio, pierde menos información respecto a la distribución verdadera. Esta interpretación resulta mucho más profunda que comparar únicamente porcentajes de acierto.

---

### La divergencia como función objetivo

Llegamos ahora a una idea muy importante. Podemos reinterpretar completamente el aprendizaje. Hasta ahora habíamos dicho que aprender consistía en ajustar parámetros. Ahora podemos expresarlo de otra manera.

```text
Datos

        ↓

Modelo

        ↓

Comparación con la realidad

        ↓

Divergencia KL

        ↓

Modificar parámetros

        ↓

Reducir KL
```

Desde esta perspectiva, todo algoritmo de aprendizaje intenta reducir progresivamente la divergencia entre el modelo y la realidad. La diferencia entre unos algoritmos y otros consiste únicamente en la forma en que realizan dicha búsqueda.

---

### Una interpretación geométrica

Aunque la divergencia KL no sea una distancia matemática, resulta útil imaginarla como una especie de "separación informacional".

```text
Modelo

        ●

             KL

                      ●

Realidad
```

Mientras mayor sea la divergencia, más diferente resulta la representación construida por el modelo. A medida que el aprendizaje avanza, esperamos que ambos puntos se acerquen progresivamente.

---

### Una conclusión importante

La divergencia de Kullback-Leibler constituye mucho más que una fórmula matemática. Representa una manera de cuantificar el costo de utilizar un modelo imperfecto para describir la realidad. Desde esta perspectiva, el aprendizaje puede interpretarse como un proceso iterativo de reducción de esa pérdida de información. Cada nuevo dato, cada actualización de parámetros y cada mejora del modelo buscan exactamente el mismo objetivo:

> **Construir una representación cuya divergencia respecto a la realidad sea lo más pequeña posible.**

En la siguiente sección descubriremos una idea aún más interesante. La divergencia KL puede descomponerse en dos componentes diferentes. Una de ellas corresponde a la **entropía** del fenómeno. La otra recibe el nombre de **entropía cruzada**. Esta descomposición permitirá comprender por qué prácticamente todas las funciones de pérdida utilizadas en clasificación corresponden, en realidad, a distintas formas de minimizar la divergencia KL.

---

Miremos el comportamiento de la divergencia KL en el siguiente libro [Libro Divergencia KL](./distancia_KL.ipynb)

## Entropía cruzada y su relación con la divergencia KL

En la sección anterior estudiamos la divergencia de Kullback-Leibler y descubrimos una idea muy importante.

> **Aprender puede interpretarse como reducir la pérdida de información entre el modelo y la realidad.**

Sin embargo, aún queda una pregunta pendiente. La expresión de la divergencia KL parece relativamente compleja.

$$
D_{KL}(P||Q)
=
\sum_x
P(x)
\log\left(
\frac{P(x)}
{Q(x)}
\right)
$$

¿Por qué precisamente esta expresión?

¿Existe alguna forma más sencilla de interpretarla?

La respuesta es afirmativa. De hecho, la divergencia KL puede separarse en dos componentes mucho más fáciles de comprender. Una de ellas corresponde a la incertidumbre propia del fenómeno. La otra representa el costo de describir dicho fenómeno utilizando un modelo. Esta segunda componente recibe el nombre de **entropía cruzada** (*Cross Entropy*)- Esta descomposición constituye uno de los resultados más importantes de la teoría de la información y del aprendizaje automático.

---

### Recordando la entropía

En una unidad anterior estudiamos el concepto de entropía de Shannon. Definimos la entropía como

$$
H(P)
=
-\sum_x
P(x)\log(P(x)).
$$

La entropía representa la cantidad promedio de información producida por un fenómeno. Cuanto mayor es la incertidumbre, mayor será la entropía. Por ejemplo, una moneda perfectamente balanceada posee mayor entropía que una moneda que casi siempre produce cara. La entropía depende únicamente del fenómeno. No depende del modelo que utilicemos para describirlo.

---

### La información esperada por el modelo

Supongamos nuevamente que el fenómeno real sigue la distribución

$$
P(x).
$$

Sin embargo,

nuestro modelo cree que la distribución correcta es

$$
Q(x).
$$

Cuando ocurre un evento, la cantidad de información que calcula el modelo será

$$
-\log(Q(x)).
$$

Observemos cuidadosamente esta expresión. Ya no aparece

$$
P(x),
$$

sino

$$
Q(x).
$$

El modelo interpreta la realidad utilizando sus propias probabilidades. Si dichas probabilidades son incorrectas, la información calculada también será incorrecta.

---

### Promediando sobre la realidad

Ahora debemos recordar una idea fundamental. Los eventos no aparecen siguiendo

$$
Q(x).
$$

Los eventos aparecen siguiendo

$$
P(x).
$$

Por tanto, la cantidad promedio de información producida por nuestro modelo será

$$
-\sum_x
P(x)
\log(Q(x)).
$$

Esta expresión recibe el nombre de **entropía cruzada**.

La escribiremos como

$$
H(P,Q).
$$

Es decir,

$$
H(P,Q)
=
-\sum_x
P(x)\log(Q(x)).
$$

---

### ¿Por qué "cruzada"?

El nombre puede parecer extraño. La razón es sencilla. La expresión mezcla dos distribuciones diferentes.

Las probabilidades reales provienen de

$$
P.
$$

Pero la información se calcula utilizando

$$
Q.
$$

En cierto sentido, estamos utilizando un modelo para describir otra distribución. Por eso hablamos de una entropía "cruzada".

---

### Comparando ambas expresiones

Ahora observemos cuidadosamente las dos definiciones.

Entropía

$$
H(P)
=
-\sum_x
P(x)\log(P(x)).
$$

Entropía cruzada

$$
H(P,Q)
=
-\sum_x
P(x)\log(Q(x)).
$$

Las expresiones son prácticamente idénticas. Existe únicamente una diferencia. En la primera, la información se calcula utilizando las probabilidades verdaderas. En la segunda, la información se calcula utilizando el modelo. Esta pequeña diferencia tendrá consecuencias enormes.

---

### Una interpretación intuitiva

Podemos interpretar ambas cantidades de la siguiente manera. La entropía responde a la pregunta

> **¿Cuánta información contiene realmente el fenómeno?**

La entropía cruzada responde a otra pregunta distinta.

> **¿Cuánta información necesita nuestro modelo para describir ese mismo fenómeno?**

Si el modelo es perfecto, ambas respuestas serán iguales. Si el modelo es incorrecto, la segunda será necesariamente mayor.

---

### El costo de utilizar un modelo imperfecto

Imaginemos nuevamente el ejemplo de la traducción. Si conocemos perfectamente un idioma, traduciremos un texto utilizando exactamente las palabras necesarias. Pero si creemos equivocadamente que el texto pertenece a otro idioma, necesitaremos realizar muchas correcciones adicionales.

El trabajo aumentará. La información necesaria también aumentará. La entropía cruzada mide precisamente ese costo adicional.

---

### Una propiedad fundamental

Existe una relación extraordinariamente importante entre estas dos cantidades. La divergencia KL puede escribirse como

$$
D_{KL}(P||Q)
=
H(P,Q)
-
H(P).
$$

Esta ecuación resume prácticamente toda la teoría del aprendizaje probabilístico. Analicemos cuidadosamente qué significa.

---

### Interpretación de la descomposición

La entropía

$$
H(P)
$$

corresponde a la incertidumbre propia del fenómeno. No podemos modificarla. Forma parte de la realidad. 

Por otra parte, la entropía cruzada

$$
H(P,Q)
$$

depende del modelo. Podemos reducirla construyendo mejores aproximaciones. La diferencia entre ambas cantidades corresponde exactamente a la pérdida de información producida por nuestro modelo. Esta pérdida es precisamente la divergencia KL.

---

### Una analogía con un examen

Imaginemos que un examen contiene cierta dificultad inherente. Ningún estudiante puede eliminar esa dificultad. Forma parte del examen. Sin embargo, un estudiante bien preparado necesitará mucho menos esfuerzo para resolverlo que otro con una preparación deficiente. La dificultad propia del examen corresponde a la entropía. El esfuerzo realizado por el estudiante corresponde a la entropía cruzada. La diferencia entre ambos representa el costo adicional producido por una preparación insuficiente. Esta diferencia es análoga a la divergencia KL.

---

### Una consecuencia muy importante

Recordemos que

$$
H(P)
$$

depende únicamente del fenómeno.

Cuando entrenamos un modelo, la realidad permanece fija. No podemos modificarla. En consecuencia, durante el aprendizaje

$$
H(P)
$$

es constante. Por tanto, la única cantidad que realmente podemos reducir es

$$
H(P,Q).
$$

Esto conduce inmediatamente a una conclusión muy importante. 

> **Minimizar la entropía cruzada equivale a minimizar la divergencia KL.**

Esta observación explica por qué la entropía cruzada aparece continuamente como función de pérdida en aprendizaje automático.

---

### Una nueva interpretación del aprendizaje

Podemos resumir el proceso completo mediante el siguiente esquema.

```text
Realidad

        ↓

Entropía H(P)
(constante)

        ↓

Modelo

        ↓

Entropía cruzada H(P,Q)

        ↓

Reducir H(P,Q)

        ↓

Reducir DKL(P||Q)
```

Desde esta perspectiva, el aprendizaje consiste simplemente en disminuir la cantidad de información adicional que necesita nuestro modelo para describir correctamente la realidad.

---

### ¿Por qué no minimizamos directamente KL?

Esta pregunta aparece con frecuencia. La respuesta resulta ahora muy sencilla. Recordemos nuevamente la igualdad

$$
D_{KL}(P||Q)
=
H(P,Q)
-
H(P).
$$

Durante el entrenamiento, la distribución verdadera

$$
P
$$

no cambia. Por tanto, la entropía

$$
H(P)
$$

es constante. Minimizar KL y minimizar la entropía cruzada producen exactamente el mismo resultado. Desde el punto de vista computacional, la entropía cruzada resulta mucho más conveniente.

Por esta razón, la mayor parte de los algoritmos modernos utilizan directamente esta función.

---

## Una visión unificada

Podemos detenernos un momento y observar el recorrido realizado hasta ahora. Primero estudiamos la entropía. Posteriormente introdujimos la divergencia KL. Ahora descubrimos la entropía cruzada. Aunque inicialmente parecían conceptos diferentes, en realidad describen distintos aspectos de una misma idea.

```text
Entropía

↓

Información propia del fenómeno

-------------------------------

Entropía cruzada

↓

Información utilizada por el modelo

-------------------------------

Divergencia KL

↓

Información adicional necesaria
debido a que el modelo es imperfecto
```

Toda esta teoría gira alrededor de una única pregunta.

> **¿Cuánta información necesitamos para describir correctamente la realidad?**

---

### Un puente hacia el aprendizaje profundo

La importancia de la entropía cruzada trasciende ampliamente la teoría de la información. Prácticamente todos los algoritmos modernos de clasificación, incluyendo las redes neuronales profundas, utilizan alguna variante de la entropía cruzada como función de pérdida. 

Durante el entrenamiento, cada actualización de los parámetros busca reducir dicha cantidad. Aunque el algoritmo parezca muy diferente, su objetivo sigue siendo exactamente el mismo. Construir un modelo cuya representación de la realidad requiera la menor cantidad posible de información adicional. En la siguiente sección veremos que esta idea conecta de manera natural con otro concepto estudiado anteriormente. 

La **máxima verosimilitud (Maximum Likelihood)** puede interpretarse también como una forma de minimizar la entropía cruzada y, por tanto, de minimizar la divergencia KL. De esta manera descubriremos que tres conceptos aparentemente independientes —Maximum Likelihood, divergencia KL y entropía cruzada— constituyen en realidad tres perspectivas diferentes de un mismo principio de aprendizaje.

---

### Cross Entropy, Maximum Likelihood y Log-Likelihood

En las secciones anteriores construimos una interpretación informacional del aprendizaje. Comenzamos definiendo la entropía como una medida de incertidumbre. Posteriormente introdujimos la divergencia de Kullback-Leibler como una forma de cuantificar la diferencia entre un modelo y la realidad. Finalmente descubrimos que la entropía cruzada representa la cantidad de información que necesita nuestro modelo para describir correctamente el fenómeno observado. Hasta aquí todo parece pertenecer a la teoría de la información. 

Sin embargo, aparece una sorpresa. Estos mismos conceptos también aparecen en la Estadística clásica. De hecho, uno de los resultados más importantes del aprendizaje automático puede resumirse en una única frase. 

> **Maximizar la verosimilitud equivale a minimizar la entropía cruzada y, por consiguiente, a minimizar la divergencia KL.**

Comprender esta afirmación significa comprender el fundamento matemático de la mayor parte de los algoritmos modernos de aprendizaje.

---

### Recordando Maximum Likelihood

En la unidad anterior estudiamos el principio de máxima verosimilitud. Supongamos que observamos un conjunto de datos

$$
x_1,x_2,\ldots,x_n.
$$

Suponemos además que dichos datos fueron generados por una distribución

$$
Q(x;\theta),
$$

cuyos parámetros

$$
\theta
$$

desconocemos. La función de verosimilitud se define como

$$
L(\theta)
=
\prod_{i=1}^{n}
Q(x_i;\theta).
$$

La idea era muy sencilla. Elegimos aquellos parámetros que hacen más probable la muestra observada.

---

### ¿Por qué utilizar logaritmos?

La likelihood suele involucrar productos de muchos términos. Cuando el número de observaciones aumenta, estos productos pueden hacerse extremadamente pequeños. Por esta razón trabajamos normalmente con la log-likelihood

$$
\ell(\theta)
=
\log L(\theta).
$$

Aplicando las propiedades de los logaritmos obtenemos

$$
\ell(\theta)
=
\sum_{i=1}^{n}
\log Q(x_i;\theta).
$$

En consecuencia, maximizar la likelihood equivale exactamente a maximizar la log-likelihood.

---

### Una interpretación diferente

Hasta este momento interpretábamos la log-likelihood como una herramienta matemática conveniente. Sin embargo, ahora podemos verla desde otra perspectiva. Cada observación aporta

$$
\log(Q(x_i)).
$$

Si el modelo asigna una probabilidad elevada al dato observado, este término será relativamente grande. Si el modelo asigna una probabilidad muy pequeña, el término disminuirá considerablemente. En otras palabras, la log-likelihood mide qué tan compatibles resultan los datos observados con el modelo propuesto.

---

### Introduciendo el signo negativo

En aprendizaje automático resulta más conveniente trabajar con funciones que deban minimizarse. Por esta razón solemos considerar

$$
-\ell(\theta).
$$

Es decir,

$$
-\ell(\theta)
=
-\sum_i
\log(Q(x_i)).
$$

A primera vista parece únicamente un cambio de signo. Sin embargo, esta expresión posee una interpretación mucho más profunda.

---

### De observaciones individuales a distribuciones

Supongamos ahora que el tamaño de la muestra es muy grande. En ese caso, la frecuencia relativa con que aparece cada valor se aproxima a su probabilidad verdadera. Es decir, en lugar de escribir

$$
-\sum_i
\log(Q(x_i)),
$$

podemos agrupar observaciones iguales. Obtenemos entonces

$$
-
N
\sum_x
P(x)
\log(Q(x)),
$$

donde

$$
N
$$

representa el tamaño de la muestra. Observemos cuidadosamente esta expresión. Dentro de la suma aparece exactamente la definición de entropía cruzada.

---

### Aparece la Cross Entropy

Recordemos nuevamente

$$
H(P,Q)
=
-
\sum_x
P(x)
\log(Q(x)).
$$

Por tanto, la log-likelihood negativa puede escribirse aproximadamente como

$$
-\ell(\theta)
\approx
N
H(P,Q).
$$

Este resultado posee una enorme importancia. La log-likelihood negativa no es otra cosa que la entropía cruzada multiplicada por el número de observaciones.

---

### Una consecuencia inmediata

Como

$$
N
$$

es constante,

minimizar

$$
-\ell(\theta)
$$

equivale exactamente a minimizar

$$
H(P,Q).
$$

Y ya demostramos anteriormente que

$$
H(P)
$$

permanece constante durante el entrenamiento. En consecuencia, también equivale a minimizar

$$
D_{KL}(P||Q).
$$

Acabamos de conectar tres conceptos que inicialmente parecían completamente independientes.

---

### Tres caminos hacia un mismo objetivo

Podemos resumir todo el razonamiento mediante el siguiente esquema.

```text
Maximum Likelihood

↓

Maximizar Log-Likelihood

↓

Minimizar Log-Likelihood Negativa

↓

Minimizar Cross Entropy

↓

Minimizar Divergencia KL
```

Aunque cada disciplina utilice un lenguaje diferente, todas persiguen exactamente el mismo objetivo. Construir un modelo que describa la realidad con la menor pérdida posible de información.

---

### Una interpretación intuitiva

Supongamos que entrenamos un clasificador de imágenes. Para una fotografía determinada, el modelo produce las siguientes probabilidades.

| Clase | Probabilidad |
|--------|-------------:|
| Gato | 0.97 |
| Perro | 0.02 |
| Caballo | 0.01 |

Si la imagen realmente corresponde a un gato, el modelo asignó una probabilidad muy alta al resultado correcto. La log-likelihood será elevada. La entropía cruzada será pequeña. La divergencia KL también será pequeña.

Ahora imaginemos otro modelo.

| Clase | Probabilidad |
|--------|-------------:|
| Gato | 0.10 |
| Perro | 0.80 |
| Caballo | 0.10 |

El modelo considera mucho más probable una clase incorrecta. La log-likelihood disminuye. La entropía cruzada aumenta. La divergencia KL también aumenta. Observemos que los tres conceptos describen exactamente el mismo comportamiento.

---

### El punto de vista de la Estadística

Desde la Estadística clásica solemos decir

> "Elegimos los parámetros que maximizan la probabilidad de los datos observados."

Esta interpretación enfatiza la compatibilidad entre el modelo y la muestra.

---

### El punto de vista de la teoría de la información

Desde la teoría de la información preferimos decir

> "Elegimos el modelo que necesita la menor cantidad posible de información adicional para describir la realidad."

Ambas afirmaciones parecen diferentes. Sin embargo, acabamos de demostrar que representan exactamente el mismo criterio de aprendizaje.

---

### El punto de vista del aprendizaje automático

En aprendizaje profundo normalmente encontramos una tercera formulación.

> "Entrenamos la red minimizando una función de pérdida denominada Cross Entropy."

Muchos estudiantes interpretan esta función como una herramienta puramente computacional. Sin embargo, ahora sabemos que posee un fundamento mucho más profundo. Minimizar la entropía cruzada significa, en realidad, construir el modelo cuya representación de la realidad produce la menor pérdida de información.

---

### Una unificación conceptual

Podemos resumir todo lo aprendido mediante una única figura.

```text
Datos observados

        ↓

Modelo probabilístico

        ↓

Likelihood

        ↓

Log-Likelihood

        ↓

Cross Entropy

        ↓

Divergencia KL

        ↓

Modelo que mejor representa
la realidad
```

A primera vista, estos conceptos pertenecen a disciplinas diferentes. Likelihood proviene de la Estadística. Cross Entropy proviene de la teoría de la información. La divergencia KL aparece tanto en Estadística como en Física y en Ciencias de la Computación. Sin embargo, todos constituyen manifestaciones distintas de un mismo principio.

---

### Una idea aún más profunda

Podemos detenernos un momento para observar el recorrido realizado desde el inicio de la unidad. Primero aprendimos que un modelo constituye una representación simplificada de la realidad. Posteriormente interpretamos esa representación como un proceso de compresión de información. Después introdujimos la divergencia KL como una medida de la calidad de dicha representación. 

Finalmente descubrimos que el entrenamiento de prácticamente todos los modelos probabilísticos consiste simplemente en reducir esa pérdida de información. Esta visión unifica gran parte de la Estadística moderna. Pero todavía queda una pregunta importante. Hasta ahora hemos supuesto que basta con reducir continuamente el error. ¿Significa esto que cuanto más complejo sea un modelo, mejor aprenderá? Sorprendentemente, la respuesta vuelve a ser negativa. En las próximas secciones descubriremos que un modelo puede aprender demasiado bien los datos de entrenamiento y, precisamente por ello, comportarse peor frente a datos nuevos. Este fenómeno recibe el nombre de **sobreajuste** (*overfitting*) y constituye uno de los conceptos más importantes del aprendizaje automático.

---

# Parte 4 — Aprender y generalizar

## Overfitting: cuando un modelo aprende demasiado

Hasta este momento hemos construido una interpretación muy completa del aprendizaje estadístico. Sabemos que aprender consiste en construir un modelo. También sabemos que dicho modelo intenta representar la realidad con la menor pérdida posible de información. Además, descubrimos que la mayoría de los algoritmos modernos buscan minimizar funciones como la entropía cruzada, la log-likelihood negativa o la divergencia de Kullback-Leibler. Podríamos pensar entonces que el problema está resuelto. 

> **Si seguimos reduciendo la función de pérdida, el modelo será cada vez mejor.**

Sorprendentemente, esta afirmación es falsa. De hecho, uno de los errores más comunes en aprendizaje automático consiste precisamente en aprender demasiado bien los datos de entrenamiento.

Este fenómeno recibe el nombre de **sobreajuste** o **overfitting**.

Comprender por qué ocurre resulta fundamental para entender qué significa realmente aprender.

---

### ¿Qué significa aprender?

Volvamos por un momento a la pregunta que ha acompañado toda esta unidad.

> **¿Qué significa aprender?**

Podríamos responder:

> Aprender consiste en construir un modelo que explique correctamente los datos.

Sin embargo, esta respuesta todavía es incompleta. Supongamos que un estudiante memoriza todas las respuestas de un examen. Cuando presenta exactamente ese mismo examen obtiene la máxima calificación. Pero si el profesor cambia ligeramente las preguntas, el estudiante ya no sabe responder. ¿Podemos decir que realmente aprendió? La mayoría de las personas respondería que no. Lo que hizo fue memorizar. No comprendió los conceptos. En aprendizaje automático ocurre exactamente lo mismo.

---

### Memorizar no es aprender

Imaginemos que entrenamos un modelo utilizando mil observaciones. Una posibilidad consiste en construir un modelo extremadamente complejo capaz de reproducir exactamente cada dato del entrenamiento. Podemos representarlo de la siguiente forma.

```text
Datos

●      ●
   ●
      ●
 ●
        ●
     ●

Modelo

~~~~~~~~~~~~~~~
~~~~~~~~~~~~~~~
~~~~~~~~~~~~~~~
```

La curva pasa exactamente por todos los puntos. El error de entrenamiento prácticamente desaparece. A primera vista parece un excelente resultado. Sin embargo, todavía no sabemos cómo responderá el modelo frente a datos nuevos.

---

### El verdadero objetivo

Cuando entrenamos un modelo no pretendemos explicar únicamente los datos que ya conocemos. Nuestro verdadero objetivo consiste en responder correctamente ante observaciones que todavía no existen. Por ejemplo, entrenamos un clasificador de imágenes utilizando miles de fotografías. Pero esperamos que posteriormente sea capaz de reconocer fotografías completamente nuevas. Entrenamos un modelo para predecir ventas utilizando información histórica. Pero esperamos que prediga correctamente las ventas del próximo mes. Entrenamos un sistema médico utilizando miles de pacientes. Pero esperamos que funcione con pacientes que aún no han llegado al hospital. En consecuencia, el verdadero objetivo del aprendizaje no consiste en recordar el pasado. Consiste en predecir correctamente el futuro.

---

#### Un ejemplo sencillo

Supongamos que observamos los siguientes datos.

```text
●

     ●

          ●

                ●

                      ●
```

A simple vista parece existir una tendencia aproximadamente lineal. Podemos ajustar una recta.

```text
●

     ●

----------●-----------

                ●

                      ●
```

El modelo no pasa exactamente por todos los puntos. Comete pequeños errores. Sin embargo, captura correctamente la tendencia general. Ahora imaginemos otro modelo.

```text
●

~~~~~●~~~~~

~~~~~~~●~~~~~~

~~~~~~~~~~●~~~~~

~~~~~~~~~~~~●~~~~
```

La curva pasa exactamente por cada observación. Su error de entrenamiento es prácticamente cero. ¿Cuál de los dos modelos será mejor? Todavía no podemos responder. Necesitamos observar datos nuevos.

---

### Entrenamiento y prueba

Para responder esta pregunta dividimos normalmente la información en dos conjuntos diferentes.

```text
Todos los datos

        │

        ├──────────────► Entrenamiento

        │

        └──────────────► Prueba
```

El conjunto de entrenamiento se utiliza para construir el modelo. El conjunto de prueba permanece oculto durante el entrenamiento. Solamente al finalizar evaluamos el comportamiento del modelo utilizando estos nuevos datos. Esta estrategia permite estimar qué tan bien generaliza el modelo.

---

### El problema aparece

Imaginemos ahora el siguiente resultado.

```text
Error de entrenamiento

0.2 %

----------------------------

Error de prueba

18 %
```

El modelo funciona extraordinariamente bien sobre los datos que ya conocía. Pero falla frecuentemente cuando aparecen nuevos ejemplos. ¿Qué ocurrió? El modelo aprendió detalles específicos del conjunto de entrenamiento que no representan realmente el fenómeno. En otras palabras, aprendió el ruido. No aprendió el patrón.

---

### Una analogía con un profesor

Imaginemos dos profesores. El primero prepara a sus estudiantes resolviendo exactamente los mismos ejercicios que aparecerán en el examen. El segundo enseña los conceptos fundamentales. Si el examen cambia ligeramente, los estudiantes del primer profesor tendrán muchas dificultades. Los del segundo probablemente responderán correctamente. El segundo profesor enseñó a generalizar. El primero enseñó únicamente a memorizar. Los modelos de aprendizaje automático enfrentan exactamente el mismo problema.

---

### Aprender el patrón o aprender el ruido

Recordemos la descomposición presentada anteriormente.

$$
Datos
=
Patrón
+
Ruido.
$$

El objetivo del aprendizaje consiste en descubrir el patrón. Sin embargo, si el modelo posee demasiada capacidad, puede comenzar a explicar incluso pequeñas fluctuaciones aleatorias. El modelo interpreta el ruido como si fuera parte del fenómeno. Esto produce un excelente desempeño sobre el entrenamiento, pero un mal comportamiento sobre nuevos datos.

---

### Una representación gráfica

Podemos ilustrar este fenómeno mediante la siguiente figura.

```text
Datos

●

     ●

          ●

               ●

                    ●


Modelo correcto

──────────────


Modelo sobreajustado

~~~~~~~~~~~~~~~
~~~~~~~
~~~~~~~~~~~~~~~
```

La primera curva describe la tendencia general. La segunda intenta seguir cada pequeña variación. Aunque parezca más precisa, generalmente produce peores predicciones.

---

### La ilusión del error cero

Muchos estudiantes creen inicialmente que el objetivo consiste en obtener un error de entrenamiento igual a cero. En realidad, esto suele ser una señal de advertencia. Cuando el modelo reproduce exactamente todos los ejemplos, existe una alta probabilidad de que también haya aprendido errores de medición, valores atípicos, o pequeñas fluctuaciones aleatorias. Reducir continuamente el error de entrenamiento no garantiza un mejor aprendizaje. En algunos casos produce exactamente el efecto contrario.

---

### ¿Por qué ocurre el sobreajuste?

El sobreajuste aparece cuando la capacidad del modelo supera ampliamente la información contenida en los datos. Podemos imaginar la siguiente situación. 

```text
Información disponible

████████

Capacidad del modelo

██████████████████████
```

El modelo dispone de mucha más capacidad de la necesaria. Como consecuencia, utiliza esa capacidad adicional para memorizar detalles accidentales. No descubre nuevas regularidades. Simplemente recuerda observaciones particulares.

---

#### Un ejemplo extremo

Supongamos que disponemos únicamente de cinco observaciones. Siempre podemos construir un polinomio de grado cuatro que pase exactamente por los cinco puntos. El error será cero. Pero si aparece una sexta observación, es muy probable que dicho polinomio produzca una predicción completamente incorrecta. El modelo aprendió perfectamente cinco ejemplos. Pero nunca aprendió el comportamiento general del fenómeno.

---

### Una nueva definición de aprendizaje

Llegamos ahora a una definición mucho más completa.

> **Aprender no consiste en minimizar el error sobre los datos observados.**

Aprender consiste en construir un modelo capaz de producir buenas predicciones sobre datos que todavía no han sido observados. Esta diferencia puede parecer pequeña. En realidad, constituye una de las ideas centrales de todo el aprendizaje automático.

---

### ¿Cómo reconocer el sobreajuste?

Una forma muy sencilla consiste en comparar dos errores.

```text
Entrenamiento

↓

Error pequeño

-------------------------

Prueba

↓

Error mucho mayor
```

Cuando ambos errores comienzan a separarse significativamente, el modelo probablemente está sobreajustando. Esta diferencia recibe frecuentemente el nombre de **brecha de generalización** (*generalization gap*).

---

### Una conclusión importante

Podemos resumir toda esta sección mediante la siguiente idea.

```text
Memorizar

↓

Excelente entrenamiento

↓

Mala generalización

-------------------------

Comprender el patrón

↓

Buen entrenamiento

↓

Buena generalización
```

El objetivo del aprendizaje nunca ha sido memorizar los datos. El objetivo consiste en descubrir las regularidades que permanecerán válidas cuando aparezcan nuevas observaciones. En la siguiente sección estudiaremos precisamente este concepto. Descubriremos qué significa **generalizar**, por qué constituye el verdadero criterio de éxito de un modelo y cómo evaluar objetivamente la capacidad de un algoritmo para enfrentarse a situaciones que nunca había observado.

---

## Generalización: el verdadero objetivo del aprendizaje

En la sección anterior estudiamos el fenómeno del **sobreajuste** (*overfitting*). Descubrimos que un modelo puede aprender perfectamente los datos de entrenamiento y, sin embargo, comportarse deficientemente cuando aparecen nuevas observaciones. Este resultado puede parecer paradójico. Después de todo, ¿no era precisamente el objetivo del entrenamiento reducir el error? 

La respuesta es sí, pero con una condición muy importante.

> **El objetivo del aprendizaje no consiste en reducir el error sobre los datos conocidos. El verdadero objetivo consiste en reducir el error sobre datos que todavía no conocemos.**

Esta idea recibe el nombre de **generalización** y constituye probablemente el concepto más importante de todo el aprendizaje automático.

---

### ¿Qué significa generalizar?

En la vida cotidiana generalizamos continuamente. Un niño no necesita ver todos los perros del mundo para aprender qué es un perro. Después de observar algunos ejemplos, es capaz de reconocer uno completamente nuevo. Un médico no necesita haber tratado exactamente al mismo paciente para formular un diagnóstico. Utiliza el conocimiento adquirido con miles de pacientes anteriores. Un ingeniero no necesita haber construido exactamente el mismo puente para diseñar uno nuevo. Generaliza principios físicos aprendidos anteriormente. En todos estos casos ocurre exactamente el mismo proceso.

A partir de un conjunto limitado de experiencias, construimos reglas suficientemente generales para enfrentarnos a situaciones nuevas. Eso es precisamente lo que esperamos de un algoritmo de aprendizaje.

---

### El futuro no está en los datos de entrenamiento

Imaginemos que entrenamos un modelo utilizando información histórica sobre el consumo eléctrico de una ciudad. Nuestro interés no consiste en explicar perfectamente los datos del año pasado. Nuestro interés consiste en estimar correctamente el consumo del próximo mes. Lo mismo ocurre con cualquier otro problema. Cuando entrenamos un detector de fraude, esperamos detectar fraudes futuros.

Cuando entrenamos un clasificador de imágenes, esperamos clasificar imágenes nuevas. Cuando entrenamos un sistema médico, esperamos diagnosticar pacientes que todavía no han llegado al hospital.

En consecuencia, el entrenamiento representa únicamente un medio. La generalización constituye el verdadero objetivo.

---

### Aprender una regla, no una lista

Podemos comprender esta idea mediante un ejemplo muy sencillo. Supongamos que un estudiante memoriza la siguiente secuencia.

```text
2

4

6

8

10
```

Si posteriormente le preguntamos cuál era el cuarto número, responderá correctamente. Pero ahora preguntamos: ¿Cuál sería el siguiente número? Si únicamente memorizó la lista, no tendrá forma de responder. En cambio, si descubrió la regla 
$$
x_n=2n,
$$

podrá generar cualquier elemento de la secuencia, incluso aquellos que nunca observó. Generalizar consiste precisamente en aprender la regla, no la lista.

---

### Entrenamiento y realidad futura

Podemos representar el proceso completo mediante el siguiente esquema.

```text
Realidad

        ↓

Datos históricos

        ↓

Entrenamiento

        ↓

Modelo

        ↓

Datos futuros

        ↓

Predicciones
```

El modelo nunca será evaluado por su capacidad para recordar el entrenamiento. Será evaluado por su capacidad para responder correctamente cuando aparezcan nuevos datos.

---

### El error que realmente importa

Hasta ahora hemos hablado del error de entrenamiento. Sin embargo, este no es el error que más nos interesa. Podemos distinguir dos cantidades diferentes. 

#### Error de entrenamiento

Mide qué tan bien el modelo explica los datos utilizados para aprender.

---

#### Error de generalización

Mide qué tan bien el modelo explica datos completamente nuevos. El primero resulta sencillo de calcular. El segundo constituye el verdadero objetivo del aprendizaje.

---

#### Una analogía con el deporte

Imaginemos un arquero que practica durante meses disparando siempre desde exactamente el mismo lugar. Con el tiempo logra acertar todas las flechas en el centro del blanco. Ahora cambia ligeramente la posición de disparo. El arquero comienza a fallar. 

¿Qué ocurrió?

Nunca aprendió realmente a lanzar. Aprendió únicamente una situación muy específica. 

Otro arquero, que entrenó desde muchas posiciones diferentes, probablemente obtendrá mejores resultados. No porque haya  memorizado más disparos, sino porque desarrolló una habilidad general. Los modelos estadísticos enfrentan exactamente el mismo desafío.

---

### ¿Por qué es tan difícil generalizar?

Generalizar implica responder correctamente ante situaciones que todavía no conocemos. Esto significa que durante el entrenamiento debemos distinguir dos componentes muy diferentes. Por una parte, existen regularidades que permanecerán válidas en el futuro. Por otra, existen detalles accidentales propios de la muestra observada.

El verdadero desafío consiste en aprender únicamente las primeras. Podemos escribir nuevamente

$$
Datos
=
Patrón
+
Ruido.
$$

Generalizar significa aprender el patrón. Memorizar significa aprender también el ruido.

---

#### La muestra representa el futuro

Esta afirmación merece una explicación. Cuando dividimos los datos en entrenamiento y prueba, el conjunto de prueba representa una simulación del futuro. El modelo nunca ha visto esos datos. Por tanto, su comportamiento sobre ellos constituye una estimación de cómo responderá cuando sea utilizado en la práctica.

Podemos imaginar el siguiente proceso.

```text
Entrenamiento

↓

Construcción del modelo

↓

Prueba

↓

Estimación del comportamiento futuro
```

En realidad, el conjunto de prueba no nos interesa por sí mismo. Nos interesa porque representa aquello que todavía no conocemos.

---

#### El error de generalización

Podemos definir ahora un nuevo concepto.

> **El error de generalización corresponde al error esperado cuando el modelo se enfrenta a observaciones nuevas provenientes del mismo fenómeno.**

Esta definición contiene una palabra muy importante.

**Esperado**.

No hablamos de un único dato. Hablamos del comportamiento promedio sobre futuros ejemplos. Esta idea conecta nuevamente con la Estadística. No nos interesa un resultado aislado. Nos interesa el comportamiento esperado del modelo.

---

#### Una representación gráfica

Imaginemos que registramos simultáneamente el error de entrenamiento y el error de prueba durante el entrenamiento.

Podemos obtener una gráfica como la siguiente.

```text
Error

│\
│ \
│  \
│   \_________________
│
│      _____________
│     /
│    /
│___/_________________________

          Tiempo de entrenamiento
```

La curva inferior representa el error de entrenamiento. Disminuye continuamente. La curva superior representa el error de prueba. Inicialmente también disminuye. Pero llega un momento en que comienza a aumentar. Ese punto marca el inicio del sobreajuste. A partir de allí, seguir entrenando mejora el entrenamiento, pero empeora la generalización.

---

#### ¿Qué significa un buen modelo?

Después de todo lo estudiado hasta ahora, podemos responder una pregunta planteada al inicio de la unidad. ¿Qué significa realmente que un modelo sea bueno? No significa que tenga el menor error de entrenamiento. No significa que memorice todos los ejemplos. No significa que posea millones de parámetros. Un buen modelo es aquel que produce buenas predicciones sobre datos que todavía no ha observado. Esta definición resume prácticamente toda la teoría moderna del aprendizaje.

---

#### Generalizar implica abstraer

Existe otra forma de interpretar exactamente la misma idea. Generalizar significa construir un nivel de abstracción. Cuando un niño aprende el concepto de árbol, no recuerda cada árbol observado. Construye una representación mental. Después reconoce árboles completamente nuevos. Cuando una red neuronal aprende a identificar rostros, no memoriza cada fotografía. Descubre patrones comunes. En ambos casos, el aprendizaje produce una abstracción. No una memoria.

---

#### El compromiso del aprendizaje

Llegamos así a una situación muy interesante. Un modelo demasiado simple no logra representar correctamente el fenómeno. Produce un elevado error estructural. Un modelo excesivamente complejo memoriza detalles accidentales. Produce sobreajuste. El verdadero desafío consiste en encontrar un punto intermedio. Podemos representarlo conceptualmente.

```text
Modelo muy simple

↓

Subajuste
(Underfitting)

----------------------------

Complejidad adecuada

↓

Buena generalización

----------------------------

Modelo muy complejo

↓

Sobreajuste
(Overfitting)
```

Todo el aprendizaje automático gira alrededor de encontrar ese equilibrio.

---

#### ¿Cómo favorecemos la generalización?

Esta pregunta ha dado origen a una enorme cantidad de técnicas desarrolladas durante las últimas décadas.

Por ejemplo,

* regularización;
* validación cruzada;
* early stopping;
* dropout;
* aumento de datos (*data augmentation*);
* selección de variables;
* poda de árboles de decisión.

Aunque parezcan técnicas muy diferentes, todas persiguen exactamente el mismo objetivo.

> **Construir modelos que generalicen mejor.**

Durante el resto de esta unidad estudiaremos las ideas matemáticas que justifican varias de estas técnicas.

---

### Una nueva interpretación del aprendizaje

Podemos resumir el recorrido realizado desde el inicio de esta unidad.

```text
Datos

↓

Modelo

↓

Aprendizaje

↓

Generalización

↓

Predicción futura
```

Observemos cuidadosamente el diagrama. El aprendizaje no constituye el final del proceso. Es únicamente el mecanismo que nos permite alcanzar el verdadero objetivo:

**generalizar correctamente**.

---

### Mirando hacia adelante

Ahora comprendemos que un modelo puede equivocarse por distintas razones. Puede tener poco poder de representación. Puede memorizar el ruido. Puede entrenarse con una muestra insuficiente. Todas estas situaciones reflejan un mismo problema. El equilibrio entre la simplicidad y la complejidad del modelo. En la siguiente sección estudiaremos precisamente este compromiso. Introduciremos dos conceptos fundamentales de la teoría del aprendizaje estadístico: 

el **sesgo (bias)** y la **varianza (variance)**.

Descubriremos que prácticamente todos los algoritmos de aprendizaje pueden entenderse como un intento de encontrar el equilibrio adecuado entre ambos extremos y que esta descomposición proporciona una de las explicaciones más profundas del fenómeno de la generalización.

---

### Bias y Varianza: el equilibrio del aprendizaje

En las secciones anteriores descubrimos que el verdadero objetivo del aprendizaje no consiste en memorizar los datos, sino en **generalizar** correctamente hacia observaciones futuras. También vimos que un modelo puede equivocarse por dos razones opuestas. Puede ser demasiado simple para representar el fenómeno. O puede ser tan complejo que termine aprendiendo incluso las pequeñas fluctuaciones aleatorias presentes en los datos. Estas dos situaciones reciben los nombres de **underfitting** y **overfitting**. Sin embargo, todavía no comprendemos completamente por qué aparecen. La respuesta proviene de uno de los conceptos más importantes del aprendizaje estadístico. El **compromiso entre sesgo (bias) y varianza (variance).** Esta idea explica por qué no existe un modelo universalmente mejor y por qué aprender consiste, en realidad, en encontrar un equilibrio.

---

#### Una analogía sencilla

Imaginemos que varias personas intentan lanzar dardos al centro de una diana.

El primer lanzador obtiene los siguientes resultados.

```text
      ●
    ●
      ●
    ●

       X
```

Todos los lanzamientos caen muy juntos.

Sin embargo, todos se encuentran desplazados respecto al centro. Ahora observemos un segundo lanzador.

```text
●

           ●


      X

               ●


   ●
```

En este caso, el promedio de los lanzamientos coincide aproximadamente con el centro. Pero existe mucha dispersión. Finalmente, consideremos un tercer lanzador.

```text
      ●
    ● X ●
      ●
```

Los lanzamientos se encuentran muy cerca del centro y presentan muy poca dispersión. Estos tres comportamientos ilustran perfectamente los conceptos de bias y varianza.

---

#### ¿Qué es el sesgo?

El **sesgo** representa un error sistemático.

Es la tendencia del modelo a producir siempre predicciones desplazadas respecto a la realidad. Podemos imaginar que el modelo observa el fenómeno utilizando unas gafas deformadas. Aunque repitamos el entrenamiento muchas veces, seguirá cometiendo aproximadamente el mismo error. En términos intuitivos, el sesgo responde a la pregunta 

> **¿Qué tan lejos, en promedio, se encuentran nuestras predicciones de la realidad?**

---

#### Un ejemplo cotidiano

Supongamos que una balanza presenta un defecto de fabricación. Cada vez que pesamos un objeto, marca exactamente dos kilogramos adicionales.

```text
Peso real

20 kg

↓

Balanza

22 kg
```

La balanza es perfectamente consistente. Siempre produce el mismo resultado. Sin embargo, siempre se equivoca en la misma dirección. Este error constituye un sesgo.

---

#### El sesgo en un modelo

Los modelos excesivamente simples presentan un comportamiento similar. Imaginemos nuevamente una relación claramente curva.

```text
Datos

        ●

     ●

  ●

       ●

             ●
```

Pero insistimos en ajustar una recta.

```text
──────────────
```

Aunque el algoritmo encuentre la mejor recta posible, seguirá existiendo una diferencia sistemática entre la realidad y el modelo. La familia de modelos simplemente no posee suficiente capacidad. Este error permanente corresponde al sesgo.

---

#### ¿Qué es la varianza?

La **varianza** representa algo completamente diferente.

No mide un desplazamiento sistemático. Mide cuánto cambia el modelo cuando cambian ligeramente los datos utilizados durante el entrenamiento. Podemos imaginar el siguiente experimento. Entrenamos el mismo algoritmo utilizando diez muestras diferentes provenientes de la misma población. Si obtenemos diez modelos prácticamente iguales, la varianza será pequeña.

Si obtenemos diez modelos completamente distintos, la varianza será elevada.

---

#### Una analogía con una opinión

Supongamos que preguntamos a una persona cuál considera la mejor película de la historia. Si responde exactamente lo mismo cada vez, su respuesta presenta poca variabilidad. 

Ahora imaginemos otra persona. Cada día responde algo completamente diferente. Su criterio resulta muy inestable.

Los modelos de aprendizaje presentan un comportamiento similar. Algunos producen prácticamente la misma solución independientemente de pequeñas variaciones en los datos. Otros cambian considerablemente ante modificaciones muy pequeñas. Estos últimos poseen una elevada varianza.

---

#### El origen de la varianza

¿Por qué ocurre este fenómeno?

Porque algunos modelos poseen una enorme capacidad de representación. Cuando el modelo dispone de muchísimos parámetros, puede adaptarse con gran facilidad a cualquier pequeño detalle de la muestra. Como consecuencia, si cambiamos ligeramente los datos, el modelo también cambia.

En otras palabras, el modelo se vuelve extremadamente sensible a la muestra utilizada durante el entrenamiento.

---

#### Dos extremos del aprendizaje

Podemos resumir las ideas anteriores mediante dos situaciones opuestas.

##### Modelos demasiado simples

* Baja capacidad.
* Elevado sesgo.
* Baja varianza.
* Underfitting.

---

##### Modelos demasiado complejos

* Alta capacidad.
* Bajo sesgo.
* Elevada varianza.
* Overfitting.

Observemos que ambos extremos producen errores, aunque por razones completamente distintas.

---

##### Una representación gráfica

Podemos imaginar la siguiente evolución.

```text
Complejidad del modelo

│

│      Bias
│\
│ \
│  \
│   \
│    \

│     \____________________

│

│                 /
│                /
│               /
│              /
│             /
│            /
│           /
│          /
│         /
│        /
│_______/________________________

          Varianza
```

A medida que aumenta la complejidad, el sesgo disminuye. Sin embargo, la varianza aumenta. Estas dos curvas se comportan en direcciones opuestas.

---

#### ¿Dónde aparece el mejor modelo?

El mejor modelo no se encuentra en ninguno de los extremos. Podemos representar la suma de ambos efectos.

```text
Error

│\
│ \
│  \
│   \
│    \______
│           \
│            \
│             \__
│_____________________________

     Complejidad
```

El error total disminuye inicialmente. Posteriormente alcanza un mínimo. Finalmente vuelve a aumentar. Ese punto mínimo representa el mejor compromiso entre sesgo y varianza.

---

#### Una interpretación intuitiva

Podemos entender este equilibrio mediante una analogía muy sencilla. Supongamos que deseamos describir un paisaje. Una posibilidad consiste en realizar un dibujo extremadamente simple.

```text
Montaña

      /\

_____/  \_____
```

Captura la idea general. Pero pierde muchos detalles. Ahora imaginemos el extremo contrario. Intentamos dibujar absolutamente cada hoja de cada árbol. El dibujo resulta extraordinariamente complejo. Pequeñas modificaciones del paisaje exigirían rehacer completamente el trabajo. El mejor dibujo probablemente se encuentre en un punto intermedio. Describe correctamente el paisaje, pero sin intentar representar cada detalle irrelevante. Los modelos estadísticos enfrentan exactamente el mismo problema.

---

#### La conexión con la información

Recordemos la interpretación desarrollada anteriormente. Aprender consiste en descubrir regularidades. No consiste en memorizar observaciones. Un modelo con elevado sesgo elimina demasiada información. La representación resulta excesivamente simple. Por el contrario, un modelo con elevada varianza conserva demasiada información, incluyendo detalles accidentales que no representan el fenómeno. Podemos interpretar ambos extremos como dos formas distintas de compresión inadecuada.

---

#### El papel del tamaño de la muestra

Existe otro aspecto muy interesante. La misma familia de modelos puede comportarse de manera diferente dependiendo de la cantidad de datos disponible. Supongamos una red neuronal muy grande. Si entrenamos utilizando únicamente cien observaciones, probablemente aparecerá una elevada varianza. Pero si disponemos de varios millones de ejemplos, esa misma red puede generalizar extraordinariamente bien. Esto significa que el equilibrio entre bias y varianza no depende  únicamente del modelo. También depende de la cantidad y la calidad de la información disponible.

---

#### ¿Cómo reducir el sesgo?

Si el problema principal consiste en un elevado sesgo, normalmente necesitamos aumentar la capacidad del modelo.

Por ejemplo, podemos:

* utilizar funciones más complejas;
* incorporar nuevas variables;
* aumentar el número de parámetros;
* utilizar arquitecturas más expresivas.

El objetivo consiste en representar mejor el fenómeno.

---

#### ¿Cómo reducir la varianza?

Si el problema principal consiste en una elevada varianza,

las estrategias suelen ser diferentes.

Podemos:

* aumentar la cantidad de datos;
* aplicar regularización;
* eliminar variables poco relevantes;
* simplificar el modelo;
* utilizar validación cruzada;
* detener el entrenamiento antes del sobreajuste (*early stopping*).

Todas estas técnicas buscan reducir la sensibilidad del modelo frente a pequeñas variaciones de la muestra.

---

#### Una visión unificada

Ahora podemos conectar prácticamente todos los conceptos estudiados durante esta unidad.

```text
Realidad

↓

Muestra

↓

Modelo

↓

Capacidad del modelo

↓

Bias

↓

Varianza

↓

Generalización
```

Observemos que todos estos conceptos aparecen como diferentes perspectivas de un mismo problema. ¿Cómo construir una representación suficientemente rica para describir el fenómeno, pero suficientemente simple para generalizar correctamente?

---

### La respuesta a la pregunta inicial

Al comienzo de esta unidad planteamos una pregunta.

> **¿Qué significa realmente aprender?**

Ahora podemos responderla con mucha mayor precisión. Aprender no consiste en memorizar observaciones. No consiste únicamente en ajustar parámetros. No consiste simplemente en minimizar una función de pérdida. Aprender consiste en construir una representación del fenómeno que capture las regularidades esenciales, ignore el ruido y mantenga el equilibrio adecuado entre sesgo y varianza para producir buenas predicciones sobre situaciones futuras.

Esta idea resume gran parte de la teoría moderna del aprendizaje estadístico. En la siguiente sección veremos cómo controlar explícitamente ese equilibrio mediante un conjunto de técnicas conocidas como **regularización**, cuyo objetivo consiste precisamente en limitar la complejidad del modelo para favorecer la generalización.

---

## Regularización: controlar la complejidad del modelo

En las secciones anteriores descubrimos una idea que puede parecer paradójica. Los modelos muy simples producen un elevado sesgo. Los modelos excesivamente complejos producen una elevada varianza. En ambos casos aparecen errores. El verdadero desafío consiste en encontrar un punto intermedio donde el modelo sea lo suficientemente expresivo para representar el fenómeno, pero no tanto como para memorizar el ruido presente en los datos. Surge entonces una pregunta natural.

> **¿Cómo podemos controlar la complejidad de un modelo durante el aprendizaje?**

La respuesta recibe el nombre de **regularización**. La regularización constituye uno de los conceptos más importantes del aprendizaje estadístico moderno y aparece prácticamente en todos los algoritmos de aprendizaje automático, desde la regresión lineal hasta las redes neuronales profundas.

---

### ¿Por qué necesitamos regularizar?

Recordemos el problema del sobreajuste. Supongamos que disponemos de un conjunto de datos relativamente pequeño. Si permitimos que el modelo sea arbitrariamente complejo, podrá adaptarse a prácticamente cualquier detalle de la muestra. Incluso pequeñas fluctuaciones producidas por ruido serán interpretadas como si formaran parte del fenómeno. Como consecuencia, el error de entrenamiento disminuirá continuamente, pero el error sobre datos nuevos comenzará a aumentar.

Podemos representar esta situación de forma intuitiva.

```text
Error

│\
│ \
│  \
│   \
│    \
│     \
│      \____________________
│
│            _________
│           /
│          /
│_________/____________________

      Complejidad
```

La regularización intenta impedir precisamente que el modelo llegue a esa región de complejidad excesiva.

---

### Una analogía cotidiana

Imaginemos que un arquitecto diseña un puente. Podría añadir vigas, refuerzos, placas, tornillos, y estructuras adicionales prácticamente sin límite. El puente sería cada vez más complejo.

Sin embargo, llegaría un momento en que esa complejidad adicional dejaría de aportar beneficios. Incluso podría aumentar el costo, el peso y la probabilidad de fallas. Un buen diseño no consiste en agregar la mayor cantidad posible de elementos. Consiste en incorporar únicamente aquellos que realmente son necesarios. Los modelos estadísticos enfrentan exactamente el mismo problema.

---

### El principio de simplicidad

La regularización se basa en una idea muy antigua en Ciencia. Entre dos modelos que explican igualmente bien un fenómeno, preferimos el más simple. Esta idea ya apareció anteriormente cuando estudiamos la Navaja de Occam. Ahora adquiere una formulación matemática. Durante el entrenamiento no solamente buscamos un modelo que explique correctamente los datos. También buscamos que dicho modelo permanezca razonablemente simple. En consecuencia, el aprendizaje deja de optimizar un único objetivo. Ahora intenta equilibrar dos objetivos simultáneamente.

---

### Dos objetivos diferentes

Podemos representar el entrenamiento mediante el siguiente esquema.

```text
Modelo

↓

Explicar correctamente los datos

+

Mantener una complejidad razonable

↓

Modelo regularizado
```

El mejor modelo ya no será necesariamente el que obtenga el menor error de entrenamiento. Será aquel que logre el mejor equilibrio entre precisión y simplicidad.

---

### Incorporando una penalización

Desde un punto de vista matemático, la regularización consiste en modificar la función de pérdida. Supongamos que inicialmente deseamos minimizar

$$
L(\theta),
$$

donde

$$
\theta
$$

representa el conjunto de parámetros del modelo. Con regularización, la nueva función objetivo se convierte en

$$
J(\theta)
=
L(\theta)
+
\lambda
\Omega(\theta).
$$

Esta expresión contiene tres componentes.

* **\(L(\theta)\)** mide qué tan bien el modelo explica los datos.

* **\(\Omega(\theta)\)** mide la complejidad del modelo.

* **\(\lambda\)** controla la importancia relativa de la penalización.

Toda la teoría de la regularización puede entenderse a partir de esta sencilla ecuación.

---

### El significado de λ

El parámetro

$$
\lambda
$$

desempeña un papel fundamental.

Si elegimos

$$
\lambda=0,
$$

la penalización desaparece. El modelo únicamente intenta minimizar el error de entrenamiento. En el extremo contrario, si

$$
\lambda
$$

es extremadamente grande, el algoritmo priorizará excesivamente la simplicidad. Obtendremos un modelo muy pequeño, pero probablemente con elevado sesgo. En consecuencia, la regularización también introduce un compromiso.

---

### Una interpretación intuitiva

Podemos imaginar

$$
\lambda
$$

como el costo asociado a la complejidad. Supongamos que cada parámetro adicional tuviera un precio. El algoritmo comenzaría entonces a preguntarse continuamente: 

> ¿Realmente necesito este parámetro para explicar los datos?

Si la respuesta es negativa, preferirá un modelo más sencillo.

---

### Regularización L2

Una de las formas más utilizadas de regularización recibe el nombre de **regularización L2** o **Ridge**. La penalización se define como

$$
\Omega(\theta)
=
\sum_i
\theta_i^2.
$$

Es decir, el algoritmo penaliza parámetros muy grandes.

¿Por qué?

Porque parámetros excesivamente grandes suelen indicar modelos demasiado sensibles a pequeñas variaciones de los datos.

Durante el entrenamiento, el algoritmo intenta mantener dichos parámetros relativamente pequeños.

---

#### Una analogía física

Imaginemos una lámina metálica unida al origen mediante pequeños resortes. Cada parámetro del modelo corresponde a una posición sobre esa lámina. Mientras el algoritmo intenta ajustar los datos, los resortes ejercen continuamente una fuerza que atrae los parámetros hacia valores moderados. No impiden el movimiento. Simplemente dificultan que los parámetros crezcan excesivamente. Esta imagen resulta bastante cercana a lo que realmente ocurre durante el entrenamiento con regularización L2.

---

### Regularización L1

Existe otra estrategia muy utilizada.

La **regularización L1**, también conocida como **Lasso**.

En este caso, la penalización viene dada por

$$
\Omega(\theta)
=
\sum_i
|\theta_i|.
$$

Aunque la expresión parece muy similar, su comportamiento es bastante diferente. Mientras L2 reduce progresivamente el tamaño de todos los parámetros, L1 tiende a llevar muchos de ellos exactamente a cero.

---

#### Selección automática de variables

Esta propiedad convierte a L1 en una herramienta muy interesante. Supongamos que construimos un modelo utilizando veinte variables. Durante el entrenamiento, la regularización L1 puede descubrir que únicamente ocho resultan realmente necesarias. Las demás reciben coeficientes exactamente iguales a cero. En consecuencia, el modelo termina realizando una selección automática de variables. Este comportamiento resulta muy útil cuando trabajamos con bases de datos de gran dimensión.

---

### Comparando ambos enfoques

Podemos resumir intuitivamente ambos métodos.

#### Regularización L2

* Reduce todos los parámetros.
* Conserva la mayoría de las variables.
* Produce modelos más estables.

---

#### Regularización L1

* Elimina completamente algunos parámetros.
* Produce modelos más pequeños.
* Realiza selección automática de variables.

Ambas técnicas buscan exactamente el mismo objetivo.

Reducir la complejidad del modelo.

---

### Regularización como control de la información

Ahora podemos conectar esta idea con la interpretación informacional desarrollada anteriormente. Recordemos que aprender consiste en construir una representación compacta de la realidad. Un modelo excesivamente complejo conserva demasiada información, incluyendo ruido y detalles accidentales.

La regularización obliga al modelo a conservar únicamente aquella información realmente necesaria para explicar el fenómeno. Desde esta perspectiva, regularizar significa controlar cuánta información puede almacenar el modelo.

---

### Una interpretación desde la compresión

Podemos imaginar nuevamente el proceso de compresión. Si permitimos que un algoritmo de compresión almacene absolutamente todos los detalles, el archivo comprimido terminará teniendo prácticamente el mismo tamaño que el original. No habremos comprimido nada. La verdadera compresión consiste en conservar únicamente la información esencial. La regularización desempeña exactamente ese papel. Obliga al modelo a distinguir entre información importante e información accidental.

---

### El papel de la experiencia

Resulta interesante observar que los seres humanos también utilizan una forma natural de regularización.

Cuando un médico aprende a diagnosticar enfermedades, no memoriza cada paciente tratado durante su vida. Extrae patrones generales. Descarta detalles irrelevantes. Conserva únicamente aquello que aparece repetidamente. En cierto sentido, nuestro cerebro regulariza continuamente el conocimiento. Si intentáramos recordar absolutamente cada detalle de cada experiencia, el aprendizaje resultaría prácticamente imposible.

---

### Regularización y generalización

Ahora podemos conectar prácticamente todos los conceptos estudiados durante esta unidad.

```text
Modelo muy complejo

↓

Memoriza el entrenamiento

↓

Alta varianza

↓

Mala generalización

---------------------------

Regularización

↓

Menor complejidad

↓

Menor varianza

↓

Mejor generalización
```

La regularización no intenta mejorar el entrenamiento. Su verdadero propósito consiste en mejorar el comportamiento futuro del modelo.

---

### La regularización en el aprendizaje profundo

Aunque hemos ilustrado estas ideas utilizando modelos relativamente sencillos, la regularización aparece también en redes neuronales profundas. Algunas técnicas ampliamente utilizadas son:

* penalización L1;
* penalización L2 (Weight Decay);
* Dropout;
* Early Stopping;
* Batch Normalization (como efecto secundario);
* Data Augmentation.

Todas ellas persiguen exactamente el mismo objetivo. Evitar que la red memorice detalles específicos del conjunto de entrenamiento.

---

### Una visión unificada

Podemos detenernos un momento y observar cómo todas las ideas desarrolladas durante esta unidad comienzan a conectarse.

```text
Datos

↓

Modelo

↓

Capacidad

↓

Bias ─────────────┐
                  │
                  ▼
            Generalización
                  ▲
                  │
Varianza ─────────┘

↓

Regularización

↓

Control de la complejidad
```

Lo que inicialmente parecía una colección de conceptos independientes comienza a formar un único marco conceptual. La complejidad, la capacidad, el sobreajuste, el sesgo, la varianza y la regularización describen distintos aspectos de un mismo problema: 

> **¿Cómo construir una representación suficientemente simple para generalizar, pero suficientemente rica para describir correctamente la realidad?**

---

### Una conclusión importante

Al comienzo de esta unidad dijimos que aprender consistía en construir un modelo. Posteriormente comprendimos que ese modelo constituye una representación comprimida de la realidad. Después descubrimos que una representación excesivamente compleja puede memorizar el ruido. Finalmente, la regularización apareció como el mecanismo que limita esa complejidad para favorecer la generalización. En otras palabras, la regularización no es simplemente una técnica matemática. Es la forma en que obligamos al modelo a aprender únicamente aquello que realmente importa. En la siguiente sección reuniremos todos los conceptos desarrollados durante la unidad para construir una interpretación unificada del aprendizaje desde la teoría de la información. Descubriremos que la Estadística, la teoría de la información y el aprendizaje automático pueden entenderse como distintas manifestaciones de un mismo principio fundamental.

---

# Parte 5 — Una visión unificada del aprendizaje

## Una interpretación informacional del aprendizaje

Al comenzar esta unidad planteamos una pregunta aparentemente sencilla.

> **¿Qué significa realmente aprender?**

A lo largo de las secciones anteriores hemos recorrido un camino considerable para responderla. Primero comprendimos que aprender consiste en construir un modelo. Después descubrimos que un modelo no representa exactamente la realidad, sino una aproximación simplificada de ella. Posteriormente analizamos las diferentes fuentes de error, estudiamos cómo medir la calidad de un modelo mediante la teoría de la información y finalmente comprendimos por qué el verdadero objetivo del aprendizaje consiste en generalizar. Ha llegado el momento de reunir todas esas ideas en una única visión. Aunque durante la unidad estudiamos muchos conceptos diferentes, todos ellos describen distintas perspectivas de un mismo fenómeno.

---

## Una mirada hacia atrás

Podemos resumir el recorrido realizado mediante una única pregunta.

> **¿Cómo pasa la realidad a convertirse en conocimiento?**

Esta transformación ocurre en varias etapas.

```text
Realidad

↓

Observaciones

↓

Datos

↓

Modelo

↓

Predicción

↓

Conocimiento
```

Cada una de estas etapas implica una pérdida de información. Y, al mismo tiempo, cada una representa un aumento en nuestra capacidad para comprender el fenómeno.

---

## La realidad contiene más información de la que podemos manejar

La realidad es extraordinariamente compleja.

Un árbol, por ejemplo, posee millones de hojas, miles de ramas, una enorme cantidad de procesos biológicos, interacciones con el viento, la humedad, la luz, el suelo, los microorganismos, los animales que viven en él. Sin embargo, cuando decimos simplemente 

> "Ese es un árbol"

hemos comprimido toda esa complejidad en una única idea. Nuestro cerebro elimina una enorme cantidad de detalles. Conserva únicamente aquello que resulta importante. Aprender consiste precisamente en realizar esa compresión.

---

## El papel de los datos

Los datos representan únicamente una pequeña ventana hacia la realidad. Nunca observamos el fenómeno completo. Observamos únicamente ejemplos. En consecuencia, todo aprendizaje comienza con información incompleta.

```text
Realidad

████████████████████████

↓

Datos

████
```

Desde el inicio aceptamos que parte de la información permanecerá desconocida. Esta fue precisamente la motivación para estudiar el error de muestreo. 

---

## El modelo como representación

Posteriormente construimos un modelo. Este modelo tampoco contiene toda la información de los datos. Conserva únicamente aquello que considera importante. 

```text
Realidad

██████████████████████

↓

Datos

██████████

↓

Modelo

████
```

Cada paso reduce la cantidad de información. Pero aumenta nuestra capacidad para comprender el fenómeno.

---

## Aprender es comprimir

Ahora podemos expresar esta idea de una forma mucho más precisa. Un modelo constituye un mecanismo de compresión. No almacena todas las observaciones. Almacena únicamente las relaciones existentes entre ellas. 

Por ejemplo, una regresión lineal no recuerda miles de observaciones. Recuerda únicamente unos pocos parámetros. 

Una distribución Normal resume millones de datos mediante 

$$
\mu
$$

y

$$
\sigma.
$$

Una red neuronal almacena millones de parámetros, pero sigue siendo infinitamente más pequeña que el conjunto de todas las experiencias posibles del mundo real. En todos los casos ocurre exactamente el mismo proceso. El conocimiento aparece como una representación compacta de la experiencia.

---

## ¿Qué significa una buena compresión?

No toda compresión resulta igualmente útil. Podemos comprimir demasiado. En ese caso, perdemos información importante. Aparece un elevado sesgo. El modelo deja de representar correctamente la realidad. También podemos comprimir muy poco. 

El modelo conserva incluso detalles accidentales. Memoriza el ruido. Aparece una elevada varianza. En consecuencia, el aprendizaje consiste en encontrar una compresión adecuada. Ni demasiada. Ni demasiado poca.

---

## El papel de la teoría de la información

La teoría de la información nos permitió responder otra pregunta. ¿Cómo medir objetivamente la calidad de una representación? La respuesta apareció mediante la divergencia de Kullback-Leibler.

```text
Realidad

↓

Distribución verdadera

↓

Modelo

↓

Divergencia KL
```

La divergencia KL cuantifica cuánta información adicional necesitamos porque nuestro modelo no coincide exactamente con la realidad. Mientras menor sea dicha cantidad, mejor será nuestra representación.

---

## Una nueva interpretación de Maximum Likelihood

Durante muchos años, Maximum Likelihood fue interpretado simplemente como un procedimiento estadístico para estimar parámetros. Ahora sabemos que representa algo mucho más profundo. Cuando maximizamos la likelihood, estamos construyendo el modelo cuya representación requiere la menor cantidad posible de información adicional. La Estadística y la teoría de la información terminan describiendo exactamente el mismo proceso.

---

## El verdadero significado de la entropía cruzada

Algo similar ocurre con la entropía cruzada. Inicialmente parecía únicamente una función de pérdida utilizada en redes neuronales. Ahora comprendemos que representa otra perspectiva del mismo fenómeno. Minimizar la entropía cruzada significa reducir la diferencia entre el modelo y la realidad. Por tanto, entrenar una red neuronal equivale, desde el punto de vista informacional, a construir una representación cada vez más eficiente del mundo.

---

## Aprender no significa recordar

Llegamos así a una conclusión muy importante. Existe una diferencia enorme entre recordar y aprender. Recordar significa conservar experiencias individuales. Aprender significa descubrir regularidades. Podemos ilustrarlo mediante una analogía sencilla. Supongamos que una persona memoriza absolutamente todas las rutas que ha recorrido en automóvil. Otra aprende únicamente las reglas generales de navegación. La primera necesitará una enorme cantidad de memoria. La segunda podrá desplazarse incluso por ciudades completamente nuevas. El aprendizaje produce flexibilidad. La memoria produce únicamente almacenamiento. Los modelos estadísticos buscan exactamente esa flexibilidad.

---

## Generalizar es la consecuencia natural

Ahora comprendemos también por qué la generalización ocupa un lugar central en el aprendizaje automático. Si el modelo descubre realmente las regularidades del fenómeno, será capaz de responder correctamente ante situaciones nuevas.

En cambio, si únicamente memoriza los ejemplos observados, fracasará cuando aparezcan nuevas observaciones. Generalizar constituye la evidencia de que el aprendizaje realmente ocurrió.

---

## Una visión desde la Ciencia

Resulta interesante observar que prácticamente todas las ciencias funcionan de esta manera. La Física no memoriza cada movimiento observado. Construye leyes generales. 

La Química no memoriza cada reacción. Construye modelos de interacción molecular.

La Biología no memoriza cada organismo. Construye teorías acerca de la evolución y el funcionamiento de los seres vivos.

La Economía no memoriza cada transacción. Construye modelos del comportamiento de los mercados.

La Ciencia siempre intenta reemplazar enormes cantidades de observaciones por unas pocas reglas generales.

En otras palabras, la Ciencia también constituye un proceso de compresión de información.

---

## Una perspectiva sobre la Inteligencia Artificial

Ahora podemos responder otra pregunta muy frecuente. ¿Qué hace realmente un sistema de Inteligencia Artificial? No memoriza simplemente grandes cantidades de datos. Intenta descubrir patrones, regularidades y relaciones ocultas.

Posteriormente utiliza dichas regularidades para producir predicciones, clasificaciones o decisiones.

Desde esta perspectiva, la Inteligencia Artificial no resulta conceptualmente diferente de la Estadística. Ambas buscan construir representaciones cada vez mejores de la realidad. Lo que cambia es la complejidad de los modelos utilizados.

---

## Una representación completa

Podemos resumir toda la unidad mediante el siguiente esquema.

```text
Realidad

↓

Observaciones

↓

Muestra

↓

Modelo

↓

Representación compacta

↓

Predicción

↓

Generalización

↓

Conocimiento
```

Cada etapa reduce la cantidad de información. Pero incrementa la capacidad para comprender el fenómeno.

---

## Una segunda representación

También podemos organizar todos los conceptos estudiados durante la unidad.

```text
Realidad

↓

Datos

↓

Modelo

↓

Compresión

↓

Entropía

↓

Cross Entropy

↓

Divergencia KL

↓

Maximum Likelihood

↓

Generalización

↓

Regularización

↓

Aprendizaje
```

Aunque inicialmente parecían conceptos independientes, todos forman parte de un único marco conceptual.

---

## La respuesta a la pregunta inicial

Podemos regresar finalmente a la pregunta que abrió esta unidad.

> **¿Qué significa realmente aprender?**

Después de todo el recorrido realizado, podemos responder de la siguiente manera. Aprender consiste en construir una representación suficientemente compacta de la realidad, capaz de conservar las regularidades fundamentales del fenómeno, eliminando el ruido y los detalles accidentales, de tal manera que sea posible realizar buenas predicciones sobre situaciones que todavía no han sido observadas. Esta definición integra prácticamente todos los conceptos desarrollados durante el capítulo.

* Los modelos.
* La inferencia.
* La teoría de la información.
* La máxima verosimilitud.
* La divergencia KL.
* La entropía cruzada.
* El sobreajuste.
* La generalización.
* La regularización.

Todos constituyen diferentes manifestaciones de un mismo principio.

---

## Un puente hacia las siguientes unidades

Esta unidad marca un cambio importante en la forma de entender el aprendizaje automático. Hasta ahora hemos estudiado los principios generales. En las próximas unidades comenzaremos a analizar algoritmos concretos. 

* Redes neuronales.
* Máquinas de soporte vectorial.
* Árboles de decisión.
* Métodos de ensamble.
* Modelos profundos.

Sin embargo, es importante recordar que todos ellos responderán exactamente a la misma pregunta. Cada algoritmo propondrá una forma diferente de construir una representación de la realidad. Cada uno utilizará distintos mecanismos de optimización. Cada uno tendrá diferentes capacidades de representación.

Pero todos compartirán un mismo objetivo.

> **Descubrir las regularidades esenciales del mundo para poder comprenderlo y predecirlo con la menor pérdida posible de información.**

Con esta idea concluye la Unidad 3.

A partir de este punto estaremos preparados para estudiar modelos de aprendizaje cada vez más complejos, entendiendo no solo cómo funcionan matemáticamente, sino también cuál es el principio informacional que justifica su existencia.

---