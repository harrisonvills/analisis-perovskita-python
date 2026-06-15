# Análisis Estadístico Multivariable: Optimización de Síntesis en Celdas Solares de Perovskita (Python)

## 1. Resumen Ejecutivo (Executive Summary)
* **El Problema:** La manufactura de semiconductores (celdas solares MAPbI3) exige un control estricto de variables físicas para maximizar la Eficiencia de Conversión de Potencia (PCE). El objetivo de este proyecto fue identificar mediante inferencia estadística qué variables del proceso de síntesis impactan significativamente el rendimiento final.
* **Herramientas:** Python (Pandas, SciPy, Statsmodels), Estadística Inferencial (Pearson, Chi-Cuadrado, T-Student de Welch, Regresión OLS).
* **Resultado Principal:** Se demostró estadísticamente que las variables de tratamiento térmico y la proporción química inicial (mezcla DMF/DMSO) son críticas, mientras que el grosor físico final de la celda no es un predictor lineal relevante para la eficiencia.

## 2. Procesamiento de Datos (Data Engineering)
* Ingesta Automatizada: Se diseñó un flujo en Python (urllib) que extrae dinámicamente la base de datos cruda desde un servidor en la nube, garantizando la reproducibilidad del código sin requerir cargas manuales por parte del usuario final.
* Se partió de una base de datos masiva (+40,000 registros), filtrando dimensionalmente el material objetivo.
* Se implementó una canalización de limpieza (ETL) manejando valores nulos y purgando métricas de eficiencia físicamente imposibles mediante el límite analítico del Rango Intercuartílico (IQR), asegurando un conjunto robusto de 6,131 observaciones.

## 3. Hallazgos Estadísticos (Key Insights)
* **Dependencia Termo-Física:** Mediante una prueba Chi-cuadrado sobre variables discretizadas ($p = 3.81 \times 10^{-5}$), se demostró una dependencia formal: las condiciones iniciales de horneado determinan el grosor final de la película semiconductora.
* **El Impacto de los Solventes:** Un análisis de varianza (T de Student para muestras heterocedásticas) sobre percentiles probó que alterar la proporción de solventes (DMF/DMSO) modifica de forma contundente la eficiencia media ($p = 1.57 \times 10^{-23}$).

## 4. Modelado Predictivo (Multivariate Analysis)
Se construyó un modelo de Regresión Lineal Múltiple para evaluar el peso simultáneo de las variables sobre el desempeño (PCE).
* **Variables Significativas ($p \le 0.001$):** La proporción de solventes, exposición térmica y temperatura inicial aportaron información relevante para el modelo.
* **Variable Descartada ($p > 0.05$):** El coeficiente asociado al espesor geométrico resultó no ser estadísticamente predictivo en este conjunto lineal.
* **Conclusión del Modelo:** El modelo OLS reportó un $R^{2}$ bajo (0.069). Esto valida una realidad industrial: la cristalización de semiconductores obedece a dinámicas no lineales complejas, lo que justifica en el futuro la transición hacia arquitecturas de Machine Learning para su predicción.
