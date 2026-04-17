# Proyecto 2 — Minería de Datos (CC3074)

Integrantes:
- Dulce Ambrosio (231143)
- Daniel Chet (231177)
- Javier Linares (231135)
- Cristian Túnchez (231359)

## Descripción

Este repositorio contiene el análisis exploratorio (EDA), limpieza, preparación de datos y el entrenamiento de modelos base para un problema de clasificación binaria de tumores (benigno vs maligno) a partir de variables citológicas.

El flujo de trabajo está documentado y es ejecutable en tres notebooks:

- `Proyecto2-S1.ipynb` (Semana 1): comprensión del problema, limpieza inicial y EDA.
- `Proyecto2-S2.ipynb` (Semana 2): preparación de datos y modelos base con evaluación.
- `Proyecto2-S3.ipynb` (Semana 3): mejora de modelos (validación cruzada, tuning) y selección del mejor modelo.

## Estructura del repositorio

- `Datos.csv`: dataset en formato CSV.
- `Proyecto2-S1.ipynb`: notebook de Semana 1 (EDA + limpieza).
- `Proyecto2-S2.ipynb`: notebook de Semana 2 (preparación + modelos base).
- `Proyecto2-S3.ipynb`: notebook de Semana 3 (mejora + selección de modelo).
- `README.md`: documentación del proyecto.

## Dataset

El archivo `Datos.csv` contiene:

- Columna identificadora: `Sample code number` (se elimina antes del análisis/modelado por no aportar valor predictivo).
- Variables predictoras (9):
	- `Clump Thickness`
	- `Uniformity of Cell Size`
	- `Uniformity of Cell Shape`
	- `Marginal Adhesion`
	- `Single Epithelial Cell Size`
	- `Bare Nuclei`
	- `Bland Chromatin`
	- `Normal Nucleoli`
	- `Mitoses`
- Variable objetivo: `Class` (2 = Benigno, 4 = Maligno).

## Limpieza de datos (resumen)

En `Proyecto2-S1.ipynb` se realiza:

- Carga del dataset y revisión de estructura (`head()`, `info()`, `describe()`).
- Inspección de valores atípicos/no numéricos en `Bare Nuclei` (en algunas versiones del dataset aparecen faltantes como `?`).
- Conversión de `Bare Nuclei` a numérico con `errors='coerce'` y eliminación de filas incompletas con `dropna()`.
- Conversión de `Class` a tipo numérico entero (garantiza valores 2/4).
- Eliminación de `Sample code number`.

En `Proyecto2-S2.ipynb` se retoma el dataset y se deja listo para modelar:

- Separación de variables predictoras `X` y objetivo `y`.
- Estandarización de características con `StandardScaler`.
- Separación de entrenamiento/prueba con `train_test_split`.

## EDA (resumen)

En `Proyecto2-S1.ipynb` se incluye:

- Distribución de clases (conteos y porcentajes).
- Histogramas de variables predictoras.
- Matriz de correlación para identificar relaciones entre variables y con la variable objetivo.
- Detección de outliers mediante boxplots.
- Boxplots de variables seleccionadas vs `Class` (p.ej. `Clump Thickness`, `Uniformity of Cell Size`, `Uniformity of Cell Shape`, `Bare Nuclei`, `Bland Chromatin`, `Mitoses`).

Hallazgos destacados (según la interpretación incluida en el notebook):

- `Uniformity of Cell Size` y `Uniformity of Cell Shape` presentan alta correlación entre sí (≈ 0.91), lo que sugiere multicolinealidad.
- `Bare Nuclei`, `Uniformity of Cell Size` y `Uniformity of Cell Shape` muestran alta correlación con `Class` (~0.82).
- `Mitoses` presenta la correlación más baja con `Class` (~0.42), indicando menor poder predictivo relativo.

## Modelos base y métricas (Semana 2)

En `Proyecto2-S2.ipynb` se entrenan y comparan modelos base:

- Regresión logística (`LogisticRegression`)
- Árbol de decisión (`DecisionTreeClassifier`)
- Random Forest (`RandomForestClassifier`)

Se reportan métricas de clasificación (con la clase positiva definida como `Class = 4`, es decir, maligno):

- Accuracy, Precision, Recall, F1
- Matriz de confusión (incluye visualización con heatmap)

## Mejora de modelos y selección (Semana 3)

En `Proyecto2-S3.ipynb` se amplía el enfoque para obtener una evaluación más robusta y mejorar el desempeño:

- Validación cruzada estratificada (k-fold) para estimar el rendimiento de los modelos de forma más confiable.
- Curvas de aprendizaje para analizar overfitting/underfitting (sesgo vs varianza).
- Afinación de hiperparámetros con `GridSearchCV`.
- Evaluación final en test set (Accuracy, Precision, Recall, F1 y AUC-ROC cuando aplica).
- Matrices de confusión y curvas ROC para comparar modelos.
- Selección del modelo priorizando **Recall** por el contexto médico (minimizar falsos negativos).

## Requisitos y ejecución

Los notebooks utilizan Python con las librerías:

- `pandas`, `numpy`
- `matplotlib`, `seaborn`
- `scikit-learn`

Para ejecutarlo localmente:

1. Crear/activar un entorno virtual (opcional pero recomendado).
2. Instalar dependencias.
3. Abrir `Proyecto2-S1.ipynb` y ejecutar las celdas en orden.
4. Abrir `Proyecto2-S2.ipynb` y ejecutar las celdas en orden.
5. Abrir `Proyecto2-S3.ipynb` y ejecutar las celdas en orden.

Ejemplo con pip:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```