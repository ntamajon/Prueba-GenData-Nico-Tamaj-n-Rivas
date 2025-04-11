# Reto de Predicción de Intrusiones Cibernéticas

## Objetivo del Reto

El objetivo de este reto es que desarrolles un modelo predictivo capaz de identificar intrusiones cibernéticas en una red a partir del conjunto de datos que te compartimos. Para ello, debes realizar un análisis exploratorio de los datos (EDA), un preprocesamiento, entrenar al menos un modelo predictivo y evaluar su rendimiento utilizando las métricas apropiadas.

**Las tareas que deberás realizar son**

1. **Análisis Exploratorio de Datos (EDA)**: Examinar el conjunto de datos para entender su distribución, relaciones entre variables, y detectar posibles valores atípicos o datos faltantes.

2. **Preprocesamiento**: Preparar los datos para el modelado, incluyendo la normalización o codificación de variables, tratamiento de valores nulos, etc.

3. **Construcción de Modelos Predictivos**: Entrenar al menos un modelo predictivo (por ejemplo, regresión logística, máquinas de soporte vectorial, árboles de decisión, etc.) para predecir la columna `attack_detected`.

4. **Evaluación del Modelo**: Evaluar el rendimiento de los modelos usando las métricas más adecuadas. 

5. **Explicación de Métricas**: Explicar cómo y por qué se utilizan estas métricas en el contexto del problema.

6. **Documentación**: Incluir una breve explicación sobre las decisiones tomadas en el proceso de modelado y evaluación.

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


## Licencia

El conjunto de datos utilizado en este reto es proporcionado por Kaggle y está disponible bajo la **Licencia MIT**. Puedes usar, modificar y distribuir este conjunto de datos de acuerdo con los términos de la licencia.

> **Fuente**: [Cybersecurity Intrusion Data (Kaggle)](https://www.kaggle.com/datasets/dnkumars/cybersecurity-intrusion-detection-dataset/data)



## Instrucciones Adicionales

- **Modelo**: Se puede usar cualquier técnica de aprendizaje automático o deep learning, pero esperamos que expliques claramente las razones de su elección.

- **Métricas**: Justificar la elección de las métricas para evaluar el modelo en el contexto de un problema de detección de intrusiones.

- **Código**: El código debe estar bien documentado, modular y fácil de seguir.


*Reto creado por: GenData*