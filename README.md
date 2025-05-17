# Estimation-of-Probability-of-Defaults-PD-for-Low-Default-Portfolios-An-Actuarial-Approach 

![Texto alternativo](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgw6QnTOfrvvSDm1h5v9AUdm9H5yVx0EiHWfjqkyuXKRwQQocoIg4lqssbrmzZeHZpAQSG2hXkv8pRZkKVNYAAlRxRjJp6W7touKt0cwbYzl4cORoxSkbE1I9MrqWjgDiFn8VGHKAMwp9O0sYLHnd0WojRn82w1fNbimvsxuEIKmJGE7CqE_f-BQA/w640-h360/Default-Probability.jpg)

Este repositorio contiene la implementación en Python de una réplica y extensión del modelo de estimación de Probabilidades de Incumplimiento (PD) presentado en el paper "Estimation of Probability of Defaults (PD) for Low-Default Portfolios: An Actuarial Approach".

##   Descripción del Modelo

El modelo tiene como objetivo estimar las PDs de manera precisa, especialmente para portafolios con baja tasa de incumplimiento (LDP), donde los métodos tradicionales pueden ser inadecuados. La metodología original, propuesta en el paper mencionado, utiliza técnicas actuariales, principalmente la convolución de distribuciones de probabilidad.

Esta implementación en Python replica la estructura principal del modelo original en lo que respecta a las convoluciones de las distribuciones de Poisson y binomial. Sin embargo, dado que el paper original no especifica la metodología exacta para obtener las PDs, se ha desarrollado un enfoque propio que incorpora los siguientes elementos clave:

* Regresiones Exponenciales: Para asegurar que las PDs sean estrictamente crecientes.
* Teorema de Bayes: Para actualizar las PDs iniciales utilizando las probabilidades empíricas del portafolio.
* Convoluciones Binomial-Poisson:
    * Una primera convolución, restringiendo la distribución binomial a un único incumplimiento, para facilitar la re-estimación bayesiana.
    * Una segunda convolución, utilizando el número total de incumplimientos reales del portafolio, para evaluar la alineación de las PDs ajustadas con la distribución real de incumplimientos.
* Combinaciones Lineales: Para combinar las PDs obtenidas por regresión exponencial con las PDs empíricas, ponderadas por los resultados de las convoluciones.
* Ajuste por Correlación: Regresiones exponenciales adicionales, realizadas por grupos de calificación, para modelar la correlación entre ellas.

##   Flujo del Modelo

1.  Replicación de Convoluciones: Se replica la metodología de convoluciones de distribuciones Poisson y binomial del paper original.
2.  Cálculo de PDs Propias: Se implementa una metodología propia para el cálculo de PDs, que incluye:
    * Convoluciones de ditribuciones Poisson y Binomial.
    * Actualización de probabilidades mediante el Teorema de Bayes.
    * Combinaciones lineales por pesos de las probabilidades de default actualizadas y empíricas.
    * Uso de regresiones exponenciales para asegurar PDs crecientes.
3.  Iteraciones de Convolución y Actualización:
    * Se realiza una primera convolución con un único incumplimiento para ajustar las PDs.
    * Se actualizan las PDs con el Teorema de Bayes.
    * Se realiza una segunda convolución con el número total de incumplimientos.
4.  Combinación y Suavizado:
    * Se combinan linealmente las PDs empíricas y las obtenidas por Bayes.
    * Se suavizan las PDs resultantes mediante regresión exponencial.
5.  Ajuste por Correlación: Se realizan regresiones exponenciales por grupos de calificación y una combinación lineal final para obtener PDs ajustadas por correlación.

##   Resultados

El modelo implementado produce resultados similares a los del paper original, validando la efectividad de la metodología propuesta para la estimación de PDs en portafolios de baja tasa de incumplimiento.
paper original: https://www.academia.edu/download/90701271/mono-2012-as12-1-iqbal.pdf
