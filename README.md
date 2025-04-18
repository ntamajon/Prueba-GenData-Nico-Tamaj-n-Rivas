# Predicción de intrusiones Cibernéticas

Utilización de modelos de Machine learning para predecir si el inicio de una sesión en un sitio web se corresponde con un ataque cibernético o no.

## Contextualización

En la era digital actual, la ciberseguridad se ha convertido en una preocupación crítica para organizaciones de todos los tamaños y sectores. Con el crecimiento exponencial del tráfico en línea y el aumento en la sofisticación de los ataques, detectar intrusiones de forma oportuna es fundamental para prevenir accesos no autorizados, pérdida de información confidencial y daños financieros. Las sesiones de red, que registran actividades como inicios de sesión, navegación y transferencia de datos, son una fuente rica de información que puede revelar comportamientos sospechosos o maliciosos.

Uno de los principales desafíos en el ámbito de la seguridad informática es la detección temprana de ataques cibernéticos entre miles o millones de sesiones aparentemente normales. Tradicionalmente, este proceso ha dependido de reglas predefinidas y supervisión humana, lo cual no es escalable ni lo suficientemente eficaz ante nuevas técnicas de ataque. Además, existen limitaciones como la ambigüedad en el comportamiento de los usuarios, la variedad de protocolos y la dificultad para distinguir entre actividades legítimas e intentos de intrusión.

En este contexto, el análisis de datos y el uso de modelos de aprendizaje automático ofrecen una solución poderosa y escalable. Al entrenar algoritmos con datos históricos de sesiones de red —que incluyen variables como tamaño de paquete, tipo de protocolo, número de intentos de inicio de sesión, reputación de IP, y si la sesión ocurrió en un horario inusual— es posible identificar patrones que predicen con alta precisión la probabilidad de un ataque. Este enfoque automatizado permite mejorar significativamente la capacidad de respuesta de los sistemas de seguridad, optimizando la detección de amenazas en tiempo real.

## Descripción del Conjunto de Datos

Este conjunto de datos contiene información sobre sesiones de red, y el objetivo es predecir si se detectó una intrusión (`attack_detected`). Las columnas del conjunto de datos son las siguientes:

1. **session_id**: Identificador único de la sesión de red.

2. **network_packet_size**: Tamaño del paquete de red en bytes.

3. **protocol_type**: Tipo de protocolo de la sesión de red (por ejemplo, TCP, UDP).

4. **login_attempts**: Número de intentos de inicio de sesión durante la sesión.

5. **session_duration**: Duración de la sesión en segundos.

6. **encryption_used**: Tipo de cifrado usado en la sesión (por ejemplo, DES, AES).

7. **ip_reputation_score**: Puntuación de reputación de la dirección IP utilizada en la sesión.

8. **failed_logins**: Número de intentos de inicio de sesión fallidos.

9. **browser_type**: Tipo de navegador usado durante la sesión.

10. **unusual_time_access**: Indicador binario (0 o 1) que indica si la sesión ocurrió en un tiempo inusual.

11. **attack_detected**: Indicador binario (0 o 1) que indica si se detectó una intrusión durante la sesión.

El conjunto de datos utilizado en este proyecto es proporcionado por Kaggle y está disponible bajo la **Licencia MIT**. Puedes usar, modificar y distribuir este conjunto de datos de acuerdo con los términos de la licencia.

> **Fuente**: [Cybersecurity Intrusion Data (Kaggle)](https://www.kaggle.com/datasets/dnkumars/cybersecurity-intrusion-detection-dataset/data)

## Metodología

 ### Análisis exploratorio:

 Se realizó una exploración inicial de los datos con visualizaciones y estadísticas descriptivas para identificar patrones, correlaciones y valores atípicos.Se usaron Pandas, Matplotlib, Numpy y Seaborn para el procesamiento y análisis.

 ### Preprocesamiento:

 Se realizaron las respectivas transformaciones numéricas, codificación de variables categóricas y generación de los conjuntos de datos para prueba y entrenamiento del modelo.

 ### Modelo predictivo:

 Usando scikit-learn, se llevó a cabo un modelo de Regresión Logística para predecir la clase predicha (1 o 0) para la variable 'attack_detected'. Se evaluó su desempeño con Accuracy Score, Recall, Precision y F1_Score.

 ### Resultados:

 Se incluye otro documento de texto con la explicación del proceso y todos los resultados.

 ## Estructura del proyecto

 Cybersecurity
├─ data
│  ├─ cybersecurity_intrusion_data.csv
│  ├─ intrusion_eda.csv
│  ├─ intrusion_encoded.csv
│  ├─ labels_test.csv
│  ├─ labels_train.csv
│  ├─ predictors_test.csv
│  └─ predictors_train.csv
├─ notebooks
│  ├─ 01_EDA.ipynb
│  ├─ 02_Preprocessing.ipynb
│  └─ 03_Logistic_Regression.ipynb
├─ README.md
└─ Results.md

## Tecnologías y Librerías Empleadas

Este proyecto fue desarrollado en Python y utiliza librerías como pandas y numpy para manipulación de datos, scikit-learn para modelado predictivo y matplotlib/seaborn para visualización. Los  análisis se realizaron en Jupyter Notebooks, y los datos fueron almacenados en archivos CSV.

## Posibles mejoras

Actualmente el modelo tiene métricas mejorables que deben ser evaluadas en conjunto, se desarrollarán árboles de decisión y Random Forests para mejorar el desempeño.

## Autores y Créditos

Este reto fue creado por GenData y desarrollado por Nicolás David Tamajón Rivas como parte de su portfolio en Data Science & Machine Learning

LinkedIn: 