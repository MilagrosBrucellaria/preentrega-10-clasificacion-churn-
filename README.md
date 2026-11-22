# Predicción de Customer Churn

## Descripción

Este proyecto fue desarrollado como parte de la Pre-Entrega 10 del curso de Data Science.

El objetivo es desarrollar y evaluar un modelo de clasificación binaria que permita predecir si un cliente abandonará o no un servicio de telecomunicaciones.

Para el análisis se utiliza el dataset Telco Customer Churn, que contiene información sobre clientes, servicios contratados, antigüedad, modalidad de contrato y cargos asociados.

La variable objetivo es `Churn`:

- `0`: el cliente permanece en el servicio.
- `1`: el cliente abandona el servicio.

## Metodología

El proyecto comprende las siguientes etapas:

1. Carga y exploración de los datos.
2. Limpieza y preparación del dataset.
3. Conversión de `TotalCharges` a formato numérico.
4. Eliminación de la variable identificadora `customerID`.
5. Transformación de la variable objetivo `Churn`.
6. División de los datos en Train/Test utilizando una proporción 80/20.
7. Preprocesamiento de variables categóricas y numéricas.
8. Entrenamiento de un modelo Logistic Regression.
9. Evaluación mediante diferentes métricas de clasificación.
10. Interpretación de los resultados desde una perspectiva de negocio.

## Modelo utilizado

Se utilizó un modelo de **Logistic Regression**.

El preprocesamiento y entrenamiento fueron integrados mediante un Pipeline de Scikit-learn.

Las variables categóricas fueron transformadas utilizando `OneHotEncoder`, mientras que las variables numéricas fueron estandarizadas mediante `StandardScaler`.

## Resultados

Los resultados obtenidos sobre el conjunto de prueba fueron:

| Métrica | Resultado |
|---|---:|
| Accuracy | 80,38 % |
| Precision | 64,85 % |
| Recall | 57,22 % |
| F1-Score | 60,80 % |

La matriz de confusión presentó los siguientes resultados:

- Verdaderos Negativos (TN): 917
- Falsos Positivos (FP): 116
- Falsos Negativos (FN): 160
- Verdaderos Positivos (TP): 214

## Interpretación

El modelo alcanzó un Accuracy de 80,38 %, mostrando un buen desempeño general de clasificación.

Sin embargo, para un problema de Customer Churn resulta especialmente relevante analizar el Recall.

El Recall obtenido fue de 57,22 %, lo que indica que el modelo identificó correctamente aproximadamente al 57 % de los clientes que efectivamente abandonaron el servicio.

La matriz de confusión mostró 160 falsos negativos. Desde el punto de vista del negocio, estos casos representan clientes que efectivamente abandonaron el servicio pero que no fueron identificados previamente como clientes en riesgo.

Por este motivo, mejorar el Recall podría permitir identificar una mayor proporción de clientes con riesgo de abandono y habilitar acciones preventivas de retención.

## Ejecución

### 1. Clonar el repositorio

```bash
git clone URL_DEL_REPOSITORIO
```

### 2. Instalar las dependencias

```bash
pip install -r requirements.txt
```

### 3. Ejecutar el notebook

Abrir:

```text
PreEntrega10-ModeladoyEvaluaciónDeClasificación.ipynb
```

y ejecutar las celdas en orden.

El archivo `Telco-Customer-Churn.csv` debe estar disponible en el mismo directorio que el notebook para realizar la carga de los datos.

## Tecnologías utilizadas

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Jupyter Notebook / Google Colab

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

## Conclusión

La Regresión Logística permitió construir un modelo inicial para identificar clientes con riesgo de abandono.

Si bien el modelo presenta un buen nivel de clasificación general, los resultados muestran una oportunidad de mejora en la detección de clientes que efectivamente realizan Churn.

En futuras iteraciones se podrían evaluar otros modelos o ajustes orientados a mejorar el Recall, buscando reducir los falsos negativos sin generar un incremento excesivo de falsos positivos.
