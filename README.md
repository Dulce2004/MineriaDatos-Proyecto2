# Proyecto 2 — Minería de Datos (CC3074)

Integrantes:
- Dulce Ambrosio (231143)
- Daniel Chet (231177)
- Javier Linares (231135)
- Cristian Túnchez (231359)

## Descripción

Este repositorio contiene el análisis exploratorio (EDA) y la limpieza inicial de un dataset de variables citológicas para un problema de clasificación binaria de tumores (benigno vs maligno). El flujo de trabajo está documentado y ejecutable en el notebook `Proyecto2.ipynb`.

## Estructura del repositorio

- `Datos.csv`: dataset en formato CSV.
- `Proyecto2.ipynb`: notebook con limpieza y EDA.
- `README.md`: documentación del proyecto.

## Dataset

El archivo `Datos.csv` contiene:

- Columna identificadora: `Sample code number` (se elimina antes del análisis/modelado por no aportar valor predictivo).
- Variables predictoras (10):
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

En `Proyecto2.ipynb` se realiza:

- Carga del dataset y revisión de estructura (`head()`, `info()`, `describe()`).
- Inspección de valores atípicos/no numéricos en `Bare Nuclei` (en algunas versiones del dataset aparecen faltantes como `?`).
- Conversión de `Bare Nuclei` a numérico con `errors='coerce'` y eliminación de filas incompletas con `dropna()`.
- Conversión de `Class` a tipo numérico entero (garantiza valores 2/4).
- Eliminación de `Sample code number`.

## EDA (resumen)

El notebook incluye:

- Distribución de clases (conteos y porcentajes).
- Histogramas de variables predictoras.
- Matriz de correlación para identificar relaciones entre variables y con la variable objetivo.
- Detección de outliers mediante boxplots.
- Boxplots de variables seleccionadas vs `Class` (p.ej. `Clump Thickness`, `Uniformity of Cell Size`, `Uniformity of Cell Shape`, `Bare Nuclei`, `Bland Chromatin`, `Mitoses`).

Hallazgos destacados (según la interpretación incluida en el notebook):

- `Uniformity of Cell Size` y `Uniformity of Cell Shape` presentan alta correlación entre sí (≈ 0.91), lo que sugiere multicolinealidad.
- `Bare Nuclei`, `Uniformity of Cell Size` y `Uniformity of Cell Shape` muestran alta correlación con `Class` (~0.82).
- `Mitoses` presenta la correlación más baja con `Class` (~0.42), indicando menor poder predictivo relativo.

## Requisitos y ejecución

El notebook utiliza Python con las librerías:

- `pandas`, `numpy`
- `matplotlib`, `seaborn`

Para ejecutarlo localmente:

1. Crear/activar un entorno virtual (opcional pero recomendado).
2. Instalar dependencias.
3. Abrir `Proyecto2.ipynb` y ejecutar las celdas en orden.

Ejemplo con pip:

```bash
pip install pandas numpy matplotlib seaborn
```