# Predicción de Customer Churn

## Descripción

Este proyecto fue desarrollado como parte de la **Pre-Entrega 10 del curso de Data Science**, enfocada en el modelado y evaluación de un problema de clasificación binaria.

El objetivo es desarrollar un modelo que permita predecir si un cliente abandonará o no un servicio de telecomunicaciones (**Customer Churn**).

Para el análisis se utiliza el dataset **Telco Customer Churn**, que contiene información sobre las características de los clientes, servicios contratados, antigüedad, modalidad de contrato y cargos asociados.

La variable objetivo es `Churn`:

- `0`: el cliente permanece en el servicio.
- `1`: el cliente abandona el servicio.

---

## Dataset

El proyecto utiliza el dataset **Telco Customer Churn**, correspondiente a un problema de abandono de clientes de una empresa de telecomunicaciones.

El archivo utilizado es:

`Telco-Customer-Churn.csv`

El dataset se encuentra incluido dentro del repositorio para permitir la reproducción completa del análisis.

Durante la preparación de los datos se detectó que la variable `TotalCharges` estaba almacenada como texto (`object`). Se realizó su conversión a formato numérico y se identificaron 11 registros con valores no convertibles, que fueron eliminados antes del entrenamiento.

Luego de la limpieza, el dataset utilizado para el modelado quedó compuesto por **7.032 registros**.

---

## Metodología

El proyecto comprende las siguientes etapas:

1. Carga y exploración inicial de los datos.
2. Limpieza y preparación del dataset.
3. Conversión de `TotalCharges` a formato numérico.
4. Eliminación de los registros no válidos detectados durante la conversión.
5. Eliminación de `customerID`, ya que corresponde únicamente a un identificador del cliente.
6. Transformación de la variable objetivo `Churn` a formato binario.
7. División de los datos en entrenamiento y prueba utilizando una proporción **80/20**.
8. Preprocesamiento de las variables categóricas y numéricas.
9. Entrenamiento de un modelo de **Logistic Regression**.
10. Generación de predicciones sobre el conjunto de prueba.
11. Evaluación mediante Accuracy, Precision, Recall, F1-Score y Matriz de Confusión.
12. Interpretación de los resultados desde una perspectiva de negocio.

La división Train/Test fue realizada utilizando `random_state=42` para garantizar la reproducibilidad y `stratify=y` para conservar la proporción de clientes con Churn en ambos conjuntos.

El resultado de la división fue:

- **Train:** 5.625 registros.
- **Test:** 1.407 registros.

La proporción de Churn se mantuvo aproximadamente en **26,58 %** en ambos conjuntos.

---

## Modelo utilizado

Se utilizó un modelo de **Logistic Regression** para resolver el problema de clasificación binaria.

El preprocesamiento y el entrenamiento fueron integrados mediante un `Pipeline` de Scikit-learn.

Las variables categóricas fueron transformadas mediante:

`OneHotEncoder`

Las variables numéricas fueron estandarizadas mediante:

`StandardScaler`

El modelo fue entrenado únicamente utilizando el conjunto de entrenamiento. Posteriormente se generaron las predicciones sobre el conjunto de prueba, que no fue utilizado durante el entrenamiento.

---

## Resultados

Las métricas obtenidas sobre el conjunto de prueba fueron:

| Métrica | Resultado |
|---|---:|
| Accuracy | 80,38 % |
| Precision | 64,85 % |
| Recall | 57,22 % |
| F1-Score | 60,80 % |

La matriz de confusión presentó los siguientes resultados:

- **Verdaderos Negativos (TN):** 917
- **Falsos Positivos (FP):** 116
- **Falsos Negativos (FN):** 160
- **Verdaderos Positivos (TP):** 214

---

## Interpretación de los resultados

El modelo alcanzó un **Accuracy de 80,38 %**, lo que indica que clasificó correctamente aproximadamente 8 de cada 10 clientes del conjunto de prueba.

Sin embargo, debido al desbalance presente en la variable objetivo, el Accuracy no debe analizarse de manera aislada.

Para la clase correspondiente a Churn, el modelo obtuvo una **Precision de 64,85 %** y un **Recall de 57,22 %**.

El Recall resulta especialmente relevante para este problema porque permite conocer qué proporción de los clientes que realmente abandonaron el servicio fue correctamente identificada por el modelo.

De los **374 clientes que efectivamente realizaron Churn**, el modelo identificó correctamente a **214**, mientras que **160 fueron clasificados incorrectamente como No Churn**.

Estos 160 casos corresponden a **falsos negativos**.

Desde el punto de vista del negocio, un falso negativo representa un cliente que realmente abandona el servicio pero que no fue identificado previamente como cliente en riesgo. Como consecuencia, podría quedar fuera de campañas de fidelización, beneficios comerciales, contactos preventivos u otras estrategias de retención.

Por este motivo, el **Recall se considera una de las métricas más relevantes para este problema**.

No obstante, mejorar el Recall también puede incrementar los falsos positivos. Por ello, resulta conveniente considerar conjuntamente Precision, Recall y F1-Score al evaluar futuras mejoras del modelo.

---

# Instrucciones de ejecución

El repositorio incluye los archivos necesarios para reproducir el análisis.

## 1. Clonar el repositorio

Copiar la URL HTTPS del repositorio público de GitHub y ejecutar:

```bash
git clone PEGAR_AQUI_LA_URL_HTTPS_DEL_REPOSITORIO
```

Luego ingresar al directorio:

```bash
cd preentrega-10-clasificacion-churn
```

> **Importante:** antes de entregar nuevamente, reemplazar `PEGAR_AQUI_LA_URL_HTTPS_DEL_REPOSITORIO` por la URL real del repositorio.

---

## 2. Instalar las dependencias

Las versiones de las librerías utilizadas se encuentran especificadas en `requirements.txt`.

Ejecutar:

```bash
pip install -r requirements.txt
```

Las principales dependencias utilizadas son:

- pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn

---

## 3. Verificar los archivos necesarios

Antes de ejecutar el análisis, verificar que el repositorio contenga:

```text
preentrega-10-clasificacion-churn/
│
├── PreEntrega10-ModeladoyEvaluaciónDeClasificación.ipynb
├── Telco-Customer-Churn.csv
├── README.md
├── requirements.txt
└── .gitignore
```

El archivo `Telco-Customer-Churn.csv` debe permanecer en el mismo directorio que el notebook debido a que el análisis realiza la carga de datos desde ese archivo.

---

## 4. Ejecutar el notebook

Abrir:

`PreEntrega10-ModeladoyEvaluaciónDeClasificación.ipynb`

El notebook puede ejecutarse utilizando **Jupyter Notebook, JupyterLab o Google Colab**.

Ejecutar las celdas en orden desde el inicio hasta el final.

Durante su ejecución, el notebook realizará:

1. Carga del dataset.
2. Exploración inicial de los datos.
3. Limpieza y preparación.
4. División Train/Test 80/20.
5. Preprocesamiento de variables categóricas y numéricas.
6. Entrenamiento de Logistic Regression.
7. Predicciones sobre el conjunto Test.
8. Cálculo de Accuracy, Precision, Recall y F1-Score.
9. Generación y visualización de la matriz de confusión.
10. Interpretación de los resultados.

Al finalizar la ejecución deben visualizarse las métricas de evaluación, el reporte de clasificación y la matriz de confusión.

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

Estas mismas versiones se encuentran especificadas en el archivo `requirements.txt`.

---

## Estructura del repositorio

```text
preentrega-10-clasificacion-churn/
│
├── PreEntrega10-ModeladoyEvaluaciónDeClasificación.ipynb
├── Telco-Customer-Churn.csv
├── README.md
├── requirements.txt
└── .gitignore
```

- **Notebook:** contiene la exploración, preparación, entrenamiento, evaluación e interpretación del modelo.
- **CSV:** contiene el dataset utilizado para el análisis.
- **README.md:** contiene la documentación e instrucciones de reproducción del proyecto.
- **requirements.txt:** especifica las dependencias y sus versiones.
- **.gitignore:** evita incorporar al repositorio archivos temporales o innecesarios generados por Python y Jupyter.

---

## Conclusión

La Regresión Logística permitió desarrollar un modelo inicial para identificar clientes con riesgo de abandono.

El modelo alcanzó un **Accuracy de 80,38 %**, aunque el análisis de las diferentes métricas muestra que todavía existe una oportunidad de mejora en la identificación de los clientes que efectivamente realizan Churn.

En particular, los **160 falsos negativos** indican que una cantidad relevante de clientes que abandonaron el servicio no fue identificada correctamente por el modelo.

Para futuras iteraciones sería recomendable evaluar alternativas que permitan mejorar el Recall sin reducir excesivamente la Precision, buscando un equilibrio entre la detección de clientes en riesgo y el costo asociado a las acciones de retención.
