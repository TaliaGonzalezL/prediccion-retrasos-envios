# Predicción de Retrasos en Envíos - Proyecto de Machine Learning

## Resumen del Proyecto

Este proyecto de portafolio demuestra un ciclo completo de ciencia de datos para resolver un problema de negocio crítico en la logística: la predicción de retrasos en las entregas. Utilizando un conjunto de datos de la cadena de suministro de DataCo, se desarrolló un modelo de **clasificación binaria** para predecir si un envío llegará a tiempo o con retraso.

El análisis abarca desde un profundo Análisis Exploratorio de Datos (EDA) para descubrir patrones, pasando por un robusto Feature Engineering, hasta el entrenamiento y la comparación de múltiples modelos de Machine Learning. El proyecto culmina con la elección de un modelo campeón (`RandomForest`) y un análisis de interpretabilidad para entender los factores clave que impulsan sus predicciones.

---

## Problema de Negocio

Los retrasos en la cadena de suministro son un problema costoso que impacta negativamente en la satisfacción del cliente, aumenta los costos operativos y puede generar penalizaciones contractuales. La capacidad de anticipar qué envíos tienen un alto riesgo de retraso permite a la empresa:

*   **Gestionar proactivamente las expectativas del cliente**, comunicando posibles demoras.
*   **Optimizar las operaciones logísticas**, asignando recursos para mitigar los riesgos identificados.
*   **Reducir costos** asociados a quejas, devoluciones y gestión de incidencias.

El objetivo de este proyecto es construir un modelo de Machine Learning que actúe como un sistema de alerta temprana, identificando los envíos propensos a retrasarse.

---

## Proceso de Análisis y Modelado

El proyecto se estructuró siguiendo las mejores prácticas de la industria:

1.  **Análisis Exploratorio de Datos (EDA):** Se investigaron las variables para encontrar patrones. Los hallazgos clave incluyeron que la tasa de retrasos varía significativamente según el **tipo de envío (`Shipping Mode`)**.

2.  **Feature Engineering:** Se crearon nuevas características a partir de las columnas de fecha para capturar patrones temporales, como `order_month`, `order_day_of_week` y, crucialmente, `order_day_of_year`.

3.  **Preprocesamiento y Pipelines:** Para asegurar un flujo de trabajo robusto y reproducible, se construyó un `Pipeline` de Scikit-Learn. Este pipeline se encarga de:
    *   **Escalar** las características numéricas con `StandardScaler`.
    *   **Codificar** las características categóricas con `OneHotEncoder`.

4.  **Experimentación de Modelos:** Se compararon dos modelos:
    *   **`LogisticRegression`** como modelo baseline.
    *   **`RandomForestClassifier`** como modelo avanzado.

5.  **Evaluación y Decisión:** La elección del modelo se basó en el **F1-Score** para la clase "Retrasado", ya que proporciona el mejor balance entre `Precision` y `Recall`. Para este problema, es más costoso no detectar un retraso (Falso Negativo) que actuar sobre una falsa alarma (Falso Positivo).

---

## Resultados y Elección del Modelo

El `RandomForestClassifier` demostró un rendimiento notablemente superior, logrando el mejor equilibrio entre la detección de retrasos y la fiabilidad de sus predicciones.

*   **Modelo Ganador:** `RandomForestClassifier`
*   **F1-Score (clase "Retrasado"): 0.70**
*   **Recall (clase "Retrasado"): 0.68** 
*   **Precision (clase "Retrasado"): 0.72**

El modelo `RandomForest` fue seleccionado por su F1-Score superior, indicando un mejor balance general. Su mayor `Recall` lo convierte en un sistema de alerta temprana más efectivo, capaz de identificar un 68% de todos los envíos que realmente se retrasan.

---

## Interpretabilidad del Modelo: ¿Qué Impulsa los Retrasos?

Para entender *por qué* el modelo toma sus decisiones, se analizó la importancia de las características (`Feature Importance`). El análisis revela que las predicciones se basan principalmente en el **valor económico de la orden** y la **estacionalidad**.

<img width="679" height="455" alt="importancia_caracteristicas" src="https://github.com/user-attachments/assets/5348ba36-024b-43e0-8483-317065e54f2b" />


Los dos factores más influyentes son:
1.  **`Sales` (Valor de la Venta):** El predictor más potente, indicando que el monto de la transacción está fuertemente correlacionado con la probabilidad de retraso.
2.  **`order_day_of_year` (Día del Año):** El segundo factor más importante, lo que confirma que existen picos de demanda estacionales (ej. temporada navideña) que impactan directamente en la logística.

Este insight permite a la empresa enfocar sus esfuerzos de mejora en la gestión de pedidos de cierto valor y en la planificación para los picos de demanda anuales.

---

## Herramientas Utilizadas

*   **Lenguaje:** Python
*   **Librerías Principales:** Pandas, NumPy, Scikit-Learn, Seaborn, Matplotlib
*   **Flujo de Trabajo:** Git, GitHub, Google Colab
