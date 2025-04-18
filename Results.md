# Explicación del proceso

## Análisis Exploratorio de Datos (EDA)

Se trata de una dataset con 11 variables, de las cuales 4 son categóricas y 7 son numéricas, sin embargo se conservan 3 de las categóricas únicamente, dado que una de estas es la variable 'session_id' el cual es un código único para cada sesión. 

En total son 9537 filas.

Lista de variables:

0   session_id           9537 non-null   object 
 1   network_packet_size  9537 non-null   int64  
 2   protocol_type        9537 non-null   object 
 3   login_attempts       9537 non-null   int64  
 4   session_duration     9537 non-null   float64
 5   encryption_used      7571 non-null   object 
 6   ip_reputation_score  9537 non-null   float64
 7   failed_logins        9537 non-null   int64  
 8   browser_type         9537 non-null   object 
 9   unusual_time_access  9537 non-null   int64  
 10  attack_detected      9537 non-null   int64  

 Se han observado valores nulos para la variable 'encryption_used', esta variable tiene sólo dos posibles valores ('DES' y 'AES') y los valores nulos representan un 20% del total, antes de decidir el tratamiento de valores nulos se estudia con qué frecuencia aparecen ambos posibles valores, resultando que el valor 'AES' está presente en el 62% de los datapoints, por lo tanto se sustituyen los valores nulos con este valor ('AES').

 Desde la matriz de correlación se ha observado en los coeficientes obtenidos que no hay evidencia de correlaciones entre variables numéricas. También observando las variables, no se evidencia que haya redundancia entre ellas.

 Para comprobar la correlación entre variables categóricas, se han obtenido los valores de "p" desde chi2_contingency, observándose que todos están muy por encima de 0.05, lo cual refiere que no hay correlación no multicolinearidad entre ellas.

 La comprobación de la correlación entre variables categóricas y numéricas se ha llevado a cabo mediante la visualización de boxplots que combinan en el eje 'x' las distintas categorías de cada variable categórica; y en el eje 'y' su combinación con cada variable numérica. Se ha observado similares características en los boxplots (medianas cercanas, rangos similares), es posible que no haya una fuerte correlación entre variables numéricas y categóricas.

 ## Transformación y escalado de datos

 ### Variables numéricas:

 #### Transformaciones

 Después de visualizar los boxplots e histogramas se ha observado que la mayoría de las variables tienen sesgo positivo, por lo que se ha decidido realizar las siguientes transformaciones, dado que el modelo a utilizar será de Regresión Logística, el cual asume normalidad:

 - *network_packet_size*: Se decide transformación boxcox después de probar con logarítmica y cuadrática y observar que se transforma en una distribución Sesgada a la izquierda
- *login_attempts*: Se decide transformación cuadrática produciendo una distribución más simétrica que la logarítmica.
- *session_duration*: Transformación boxcox
- *ip_reputation_score*: Transformación boxcox
- *failed_logins*: Transformación logarítmica que soporta ceros
- *unusual_time_access*: Sin transformar
- *attack_detected*: Sin transformar

#### Escalado

Variables numéricas escaladas por estandarización

### Variables categóricas

Se ha realizado One-hot Encoding

## Modelo de Regresión Logística

1) Revisión del balance de clases, resultando 55% clase 0 (ataque detectado positivo) y 45% clase 1 (ataque detectado negativo)

2) En la primera corrida del modelo de regresión logística (80/20), sin regularización (penalty = None) se obtiene la siguiente matriz de confusión:

- True Positives = 824
- False Positives = 366
- False Negatives = 218
- True Negatives = 500

3) Se obtienen las siguientes métricas de evaluación en la muestra de prueba

- Accuracy Score, % total de predicciones correctas sobre todos los casos: 0.6939203354297694
- Precision Score, % de positivos predichos por el modelo: 0.6963788300835655
- Recall score % de positivos encontrados por el modelo respecto a los reales: 0.5773672055427251
- f1 score: 0.6313131313131313 

Al comparar con las métricas en la muestra de entrenamiento los comportamientos resultan similares, se descarta posible overfitting.

Se observa que el recall es bajo

El comportamiento ideal del modelo, dado que el objetivo es predecir ataques, será el no pasar por alto ningún ataque cibernético (Recall alto)

4) Optimización de hiperparámetros

Optimización del parámetro C con GridSearch Cross-Validation para regularización L1 Ridge.
Se obtiene:

Mejor C: {'C': 0.002257019719633919}
Mejor recall (CV): 0.6989474140171532

Se desarrolla un bucle para encontrar el mejor umbral de predicción, dado que que la intención es incrementar la detección de positivos aunque se pierda un poco de precisión.

Se obtiene un umbral de 1% en el bucle, el cual se descarta, puesto que con un umbral de 0.01 (1%) 99% de las sesiones serían clasificadas como ataques (incremento de falsos positivos) 

Se grafican las siguientes curvas:
- Curva ROC + AUC para comportamiento del modelo: Buena separabilidad de las clases.

- Umbral vs F1 Score: importa detectar positivos (recall) sin disparar muchos falsos positivos (precisión)
F1 = 2x[precision*recall/(precision+recall)]

Se busca el umbral que maximiza F1

Modelo final con umbral = 0.38.

La regularización L1 se descarta, ya que C=0.002 es extremadamente restrictivo y al evaluar se pierde mucha precisión (cae a 0,49, casi detección al azar)

Se obtienen las siguientes métricas finales:

Datos de prueba
Accuracy Score, % total de predicciones correctas sobre todos los casos: 0.6336477987421384
Precision Score, % de positivos predichos por el modelo: 0.572419774501301
Recall score % de positivos encontrados por el modelo respecto a los reales: 0.7621247113163973
f1 score: 0.6313131313131313


