#  Unsupervised Learning Workshop – Mushroom Dataset

##  Descripción del Proyecto

Este proyecto desarrolla un flujo completo de análisis y modelado sobre el **Mushroom Dataset** del UCI Repository, con el objetivo de:

- Transformar un dataset categórico complejo en una matriz apta para modelado.
- Analizar patrones estructurales mediante técnicas estadísticas y visuales.
- Aplicar **reducción de dimensionalidad (PCA)**.
- Detectar estructuras latentes con **K-Means Clustering**.
- Comparar los resultados de aprendizaje no supervisado con un modelo supervisado (**Random Forest**).

El proyecto está estructurado en tres notebooks independientes que siguen un pipeline lógico:

1. Limpieza y transformación  
2. Análisis exploratorio (EDA)  
3. Modelado y comparación  

---

#  Dataset

🔗 UCI Mushroom Dataset  

- Cada fila representa un hongo.  
- Todas las variables son categóricas nominales.  
- Variable objetivo:  
  - `e` → edible  
  - `p` → poisonous  

---

#  Estructura del Proyecto

| Archivo | Descripción |
|----------|-------------|
| `cleaning.ipynb` | Limpieza, tipado y transformación inicial del dataset |
| `eda.ipynb` | Análisis exploratorio univariado, bivariado y multivariado |
| `machine_learning.ipynb` | Modelado con PCA, KMeans y Random Forest |
| `data/clean/agaricus-lepiota` | Dataset limpio exportado |

---

# 1️ Limpieza y Transformación (`cleaning.ipynb`)

##  Carga y estructuración

- Asignación manual de nombres de columnas según documentación oficial.
- Conversión de variables a tipo `category`.
- Mapeo semántico de valores (ej. `p` → poisonous).

##  Limpieza aplicada

- Eliminación de columna constante (`veil-type`).
- Detección y análisis de valores nulos.
- Imputación de valores faltantes en `stalk-root` usando la moda.
- Validación de unicidad y estructura final.

##  Exportación

El dataset limpio se exporta para su uso posterior en formato parquet.

---

# 2️ Análisis Exploratorio (EDA) (`eda.ipynb`)

El EDA se desarrolla en tres niveles:

##  Análisis Univariado

- Distribución de la variable objetivo.
- Conteo de categorías por variable.
- Identificación de dominancias y posibles sesgos.

##  Análisis Bivariado

- Comparación de cada variable respecto a la clase (edible vs poisonous).
- Visualización de proporciones.
- Identificación de variables con alta capacidad discriminatoria.

##  Análisis Multivariado

- Test Chi-cuadrado para medir asociación entre variables y la clase.
- Ranking de fuerza estadística.
- Identificación de predictores clave (ej. `odor`).

###  Hallazgos principales

- Algunas variables muestran una separación casi determinista entre clases.
- El olor aparece como uno de los predictores más fuertes.
- Las combinaciones de variables mejoran la discriminación frente a variables aisladas.

---

# 3️ Modelado y Machine Learning (`machine_learning.ipynb`)

##  Preprocesado

- Conversión de variable objetivo a formato binario (LabelEncoder).
- One-Hot Encoding sobre variables categóricas.
- Separación en `X` e `y`.
- División en train/test (80/20).
- Uso consistente de `random_state=42`.

---

##  PCA – Reducción de Dimensionalidad

- Aplicación de PCA para visualización en 2 componentes.
- Evaluación del impacto del número de componentes en rendimiento.
- Estudio del trade-off entre dimensionalidad y accuracy.
- Análisis del rendimiento del modelo con distintos números de componentes (2 a 28).

---

##  Random Forest (Modelo Supervisado)

- Entrenamiento con todas las features codificadas.
- Evaluación de accuracy.
- Comparación:
  - Random Forest sin PCA.
  - Random Forest con PCA reducido.

###  Objetivo

Determinar si la reducción de dimensionalidad mantiene la señal predictiva sin degradar el rendimiento.

---

##  Clustering con K-Means (No Supervisado)

- Determinación del número óptimo de clusters.
- Entrenamiento con:
  - Features originales.
  - Features reducidas por PCA.
- Visualización de clusters en 2D.
- Comparación entre clusters y clases reales (sin usar etiquetas durante entrenamiento).

###  Evaluación conceptual

Se analiza la correspondencia entre clusters y etiquetas reales para evaluar:

- Si la estructura natural del dataset separa correctamente setas comestibles y venenosas.
- Si el problema puede abordarse desde segmentación no supervisada.

---

#  Comparativa Final

| Modelo | Tipo | Uso de PCA | Objetivo |
|--------|------|------------|----------|
| Random Forest | Supervisado | No | Línea base |
| Random Forest | Supervisado | Sí | Evaluar reducción |
| K-Means | No supervisado | Sí/No | Descubrir estructura latente |

---

#  Conclusiones

- El dataset presenta variables con alta capacidad discriminatoria.
- La reducción con PCA permite compresión significativa manteniendo rendimiento.
- El clustering muestra estructuras que parcialmente coinciden con las clases reales.
- El aprendizaje no supervisado puede aproximarse al problema, pero el modelo supervisado ofrece mayor precisión.

Este proyecto demuestra:

- Dominio del flujo completo de Data Science.
- Gestión avanzada de variables categóricas.
- Aplicación combinada de técnicas supervisadas y no supervisadas.
- Capacidad de análisis estadístico e interpretación de resultados.

---

#  Tecnologías Utilizadas

- Python 3.10+
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn:
  - PCA
  - KMeans
  - RandomForestClassifier
  - Train/Test Split
  - OneHotEncoder
  - LabelEncoder

---

#  Instalación y Ejecución

```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook
