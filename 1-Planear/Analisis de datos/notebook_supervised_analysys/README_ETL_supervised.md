# Proceso ETL (Extracción, Transformación y Carga) – ECOLUZ Análisis

## Importación de librerías

Librerías utilizadas para la conexión, manipulación, visualización y modelado supervisado.

```python
import pandas as pd                     # Manipulación y análisis de datos en DataFrames
import numpy as np                      # Operaciones matemáticas y numéricas

# Visualización
import matplotlib.pyplot as plt         # Gráficos estáticos
import seaborn as sns                   # Visualización estadística avanzada

# Conexión con base de datos MongoDB
from dotenv import load_dotenv          # Carga de variables de entorno desde archivo .env
from pymongo import MongoClient         # Conexión y consultas a MongoDB

# Machine Learning supervisado
from sklearn.model_selection import train_test_split   # División train/test
from sklearn.preprocessing import LabelEncoder         # Codificación de variables categóricas
from sklearn.tree import DecisionTreeClassifier, plot_tree   # Árboles de decisión
from sklearn.ensemble import RandomForestClassifier           # Random Forest
from sklearn.metrics import classification_report, confusion_matrix  # Métricas de evaluación
from sklearn.decomposition import PCA                   # Reducción de dimensionalidad

import os                               # Manejo de rutas y sistema de archivos
```

---

## Conexión y carga de datos desde MongoDB

Extracción de registros desde la colección luminarias.

```python
load_dotenv()
MONGO_URI = os.getenv("CONECTION_DB")

def export_mongo_sample_to_csv(db_name, collection_name, out_csv="dataset_sample.csv", sample_size=5000, projection=None):
	if os.path.exists(out_csv):
		df = pd.read_csv(out_csv)
		return df
	client = MongoClient(MONGO_URI)
	col = client[db_name][collection_name]
	pipeline = [{"$sample": {"size": sample_size}}]
	if projection:
		pipeline.append({"$project": projection})
	cursor = col.aggregate(pipeline)
	data = list(cursor)
	df = pd.json_normalize(data)
	df.to_csv(out_csv, index=False)
	client.close()
	return df

df = export_mongo_sample_to_csv("luminarias", "luminarias", "dataset_sample.csv", 5000)
```

---

## Creación del DataFrame

Inspección inicial de datos.

```python
df.head()
df.info()
df.describe()
```

---

## Preparación y limpieza de datos

Procesos de depuración y codificación.

```python
# Eliminación de duplicados y valores nulos
df_clean = df.drop_duplicates().dropna()

# Codificación de variables categóricas
labelencoder = LabelEncoder()
df_clean["brand_encoded"] = labelencoder.fit_transform(df_clean["brand"].astype(str))
```

---

## División en entrenamiento y prueba

Separación de dataset para entrenamiento supervisado.

```python
X = df_clean[["brand_encoded", "reviews.rating", "reviews.numHelpful"]]
y = df_clean["categories"]

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)
```

---

## Modelado supervisado (Árboles y Random Forest)

Entrenamiento de modelos de clasificación.

```python
# Árbol de decisión
dt_model = DecisionTreeClassifier(max_depth=5, random_state=42)
dt_model.fit(X_train, y_train)
y_pred_dt = dt_model.predict(X_test)

# Random Forest
rf_model = RandomForestClassifier(n_estimators=100, random_state=42)
rf_model.fit(X_train, y_train)
y_pred_rf = rf_model.predict(X_test)
```

---

## Evaluación de modelos

Métricas de desempeño y matriz de confusión.

```python
print("Reporte de clasificación - Árbol de decisión")
print(classification_report(y_test, y_pred_dt))

print("Reporte de clasificación - Random Forest")
print(classification_report(y_test, y_pred_rf))

cm = confusion_matrix(y_test, y_pred_rf)
sns.heatmap(cm, annot=True, fmt="d", cmap="Blues")
plt.title("Matriz de Confusión - Random Forest")
plt.show()
```

---

## Visualización de árbol de decisión

Representación gráfica del modelo entrenado.

```python
plt.figure(figsize=(16, 8))
plot_tree(dt_model, feature_names=X.columns, class_names=list(y.unique()), filled=True)
plt.show()
```

---

## Exportación del dataset procesado

Guardado de los datos preparados.

```python
df_clean.to_csv("data/processed/amazon_supervised_clean.csv", index=False)
```

---

## Conclusión de esta fase

En esta fase de ETL y análisis supervisado, se extrajeron datos desde MongoDB, se limpiaron y codificaron variables categóricas, para posteriormente entrenar y evaluar modelos de clasificación como Árbol de Decisión y Random Forest.

Los resultados obtenidos permiten identificar patrones en los datos y evaluar el rendimiento de los algoritmos mediante métricas de clasificación y matrices de confusión.g