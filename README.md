# Predicción de Customer Churn

## Descripción

Este proyecto fue desarrollado como parte de la **Pre-Entrega 10 del curso de Data Science**, enfocada en el modelado y evaluación de un problema de clasificación binaria.

El objetivo es desarrollar y evaluar un modelo que permita predecir si un cliente abandonará o no un servicio de telecomunicaciones (Customer Churn).

Para el análisis se utiliza el dataset **Telco Customer Churn**, que contiene información sobre las características de los clientes, los servicios contratados, la antigüedad, la modalidad de contrato y los cargos asociados.

La variable objetivo es `Churn`:

- `0`: el cliente permanece en el servicio.
- `1`: el cliente abandona el servicio.

---

## Dataset

El archivo utilizado para el análisis es:

`Telco-Customer-Churn.csv`

El dataset se encuentra incluido dentro del repositorio para permitir la reproducción completa del análisis.

Originalmente el dataset contiene **7.043 registros**.

Durante la preparación de los datos se detectó que la variable `TotalCharges`, que representa un valor numérico, se encontraba almacenada como texto (`object`). Se realizó su conversión a formato numérico y se identificaron **11 registros con valores no convertibles**, que fueron eliminados antes del entrenamiento.

Luego de la limpieza, el dataset utilizado para el modelado quedó compuesto por **7.032 registros**.

---

## Metodología

El proyecto comprende las siguientes etapas:

1. Carga y exploración inicial de los datos.
2. Limpieza y preparación del dataset.
3. Conversión de `TotalCharges` a formato numérico.
4. Eliminación de los registros no válidos detectados durante la conversión.
5. Eliminación de `customerID`, debido a que corresponde únicamente a un identificador único del cliente.
6. Transformación de la variable objetivo `Churn` a formato binario.
7. Separación entre variables predictoras (`X`) y variable objetivo (`y`).
8. División de los datos en entrenamiento y prueba utilizando una proporción **80/20**.
9. Preprocesamiento de variables categóricas y numéricas.
10. Entrenamiento de un modelo de **Logistic Regression**.
11. Generación de predicciones sobre el conjunto de prueba.
12. Evaluación mediante Accuracy, Precision, Recall, F1-Score y Matriz de Confusión.
13. Interpretación de los resultados desde una perspectiva de negocio.

### División Train/Test

La división se realizó utilizando `random_state=42` para garantizar la reproducibilidad del experimento y `stratify=y` para conservar la distribución de la variable objetivo.

El resultado fue:

- **Train:** 5.625 registros (80 %).
- **Test:** 1.407 registros (20 %).
- **Proporción de Churn en Train:** 26,58 %.
- **Proporción de Churn en Test:** 26,58 %.

Los conjuntos de entrenamiento y prueba son generados directamente dentro del notebook mediante `train_test_split`, por lo que no se requieren archivos adicionales de Train o Test.

---

## Modelo utilizado

Para resolver el problema de clasificación binaria se utilizó un modelo de **Regresión Logística (Logistic Regression)**.

El preprocesamiento y el entrenamiento fueron integrados mediante un `Pipeline` de Scikit-learn.

Las variables categóricas fueron transformadas mediante `OneHotEncoder`, mientras que las variables numéricas fueron estandarizadas utilizando `StandardScaler`.

El modelo fue entrenado únicamente con el conjunto de entrenamiento. Posteriormente, se generaron las predicciones sobre el conjunto de prueba, que no fue utilizado durante el entrenamiento.

---

## Resultados

Las métricas obtenidas sobre el conjunto de prueba fueron:

| Métrica | Resultado |
|---|---:|
| Accuracy | 80,38 % |
| Precision | 64,85 % |
| Recall | 57,22 % |
| F1-Score | 60,80 % |

### Matriz de Confusión

La matriz de confusión presentó los siguientes resultados:

- **Verdaderos Negativos (TN):** 917
- **Falsos Positivos (FP):** 116
- **Falsos Negativos (FN):** 160
- **Verdaderos Positivos (TP):** 214

---

## Interpretación de los resultados

El modelo alcanzó un **Accuracy de 80,38 %**, lo que indica que clasificó correctamente aproximadamente 8 de cada 10 clientes del conjunto de prueba. Sin embargo, debido al desbalance existente en la variable objetivo, el Accuracy no debe analizarse de manera aislada.

Para la clase correspondiente a Churn, el modelo obtuvo una **Precision de 64,85 %**. Esto significa que, entre los clientes identificados por el modelo como posibles abandonos, aproximadamente el 65 % efectivamente abandonó el servicio.

El **Recall fue de 57,22 %**, indicando que el modelo logró identificar correctamente aproximadamente al 57 % de los clientes que realmente abandonaron el servicio.

De los **374 clientes que efectivamente realizaron Churn**, el modelo identificó correctamente a **214**, mientras que **160 fueron clasificados incorrectamente como No Churn**. Estos últimos corresponden a los falsos negativos.

Desde el punto de vista del negocio, los falsos negativos representan un costo potencial importante. Un cliente que realmente está próximo a abandonar pero que el modelo no identifica podría quedar fuera de campañas de fidelización, beneficios comerciales, contactos preventivos u otras acciones de retención.

Por este motivo, para este problema se considera al **Recall como una de las métricas más relevantes**. Un aumento del Recall permitiría detectar una mayor proporción de clientes que efectivamente abandonarán el servicio.

Sin embargo, el Recall no debe analizarse de forma aislada. Incrementarlo puede generar también un aumento de falsos positivos y, por lo tanto, acciones de retención sobre clientes que no tenían intención de abandonar. El **F1-Score de 60,80 %** permite complementar el análisis considerando conjuntamente Precision y Recall.

---

# Instrucciones de ejecución

El repositorio incluye los archivos necesarios para reproducir el análisis.

## 1. Clonar el repositorio

Ejecutar en una terminal:

```bash
git clone https://github.com/MilagrosBrucellaria/preentrega-10-clasificacion-churn-.gi
```

Luego ingresar al directorio del proyecto:

```bash
cd preentrega-10-clasificacion-churn-
```

## 2. Instalar las dependencias

Ejecutar:

```bash
pip install -r requirements.txt
```

El archivo `requirements.txt` contiene las versiones de las librerías utilizadas durante el desarrollo del proyecto.

## 3. Verificar los archivos

El repositorio contiene los siguientes archivos necesarios para reproducir el análisis:

```text
preentrega-10-clasificacion-churn-/
│
├── PreEntrega10-ModeladoyEvaluaciónDeClasificación.ipynb
├── Telco-Customer-Churn.csv
├── README.md
├── requirements.txt
└── .gitignore
```

El archivo `Telco-Customer-Churn.csv` debe permanecer en el mismo directorio que el notebook para que la carga de datos se realice correctamente.

No es necesario disponer de archivos Train y Test separados, ya que ambos conjuntos son generados automáticamente dentro del notebook mediante una división estratificada 80/20.

## 4. Ejecutar el notebook

Abrir:

`PreEntrega10-ModeladoyEvaluaciónDeClasificación.ipynb`

El notebook puede ejecutarse utilizando **Jupyter Notebook, JupyterLab o Google Colab**.

Ejecutar todas las celdas en orden, desde el inicio hasta el final.

Durante la ejecución se realizan automáticamente las siguientes etapas:

1. Carga del dataset.
2. Exploración inicial.
3. Limpieza y preparación de los datos.
4. División Train/Test 80/20.
5. Preprocesamiento de variables.
6. Entrenamiento de Logistic Regression.
7. Predicciones sobre el conjunto Test.
8. Cálculo de Accuracy, Precision, Recall y F1-Score.
9. Generación del reporte de clasificación.
10. Generación y visualización de la matriz de confusión.
11. Interpretación de los resultados.

Al finalizar la ejecución se visualizarán las métricas de evaluación y la matriz de confusión utilizadas para analizar el desempeño del modelo.

---

## Dependencias

Las versiones utilizadas durante el desarrollo fueron:

```text
pandas==2.2.3
numpy==2.2.6
matplotlib==3.10.0
seaborn==0.13.2
scikit-learn==1.6.1
```

Estas mismas versiones se encuentran especificadas en `requirements.txt`.

---

## Estructura del repositorio

```text
preentrega-10-clasificacion-churn-/
│
├── PreEntrega10-ModeladoyEvaluaciónDeClasificación.ipynb
├── Telco-Customer-Churn.csv
├── README.md
├── requirements.txt
└── .gitignore
```

### Contenido de los archivos

- **`PreEntrega10-ModeladoyEvaluaciónDeClasificación.ipynb`:** contiene la exploración, preparación, entrenamiento, evaluación e interpretación del modelo.
- **`Telco-Customer-Churn.csv`:** dataset utilizado para el análisis.
- **`README.md`:** documentación del proyecto e instrucciones completas de ejecución.
- **`requirements.txt`:** dependencias del proyecto con sus versiones.
- **`.gitignore`:** exclusiones de archivos temporales y archivos innecesarios generados por Python y Jupyter.

---

## Conclusión

La Regresión Logística permitió desarrollar un modelo inicial para identificar clientes con riesgo de abandono.

El modelo alcanzó un **Accuracy de 80,38 %**, aunque desde una perspectiva de negocio existe una oportunidad de mejora en la identificación de clientes que efectivamente realizan Churn.

En particular, los **160 falsos negativos** muestran que una cantidad relevante de clientes que abandonaron el servicio no fue identificada correctamente por el modelo.

Por este motivo, en futuras iteraciones sería recomendable evaluar alternativas que permitan mejorar el Recall sin reducir excesivamente la Precision, buscando un equilibrio entre la detección de clientes en riesgo y el costo asociado a las acciones de retención.

Para futuras iteraciones sería recomendable evaluar alternativas que permitan mejorar el Recall sin reducir excesivamente la Precision, buscando un equilibrio entre la detección de clientes en riesgo y el costo asociado a las acciones de retención.
