# Proceso ETL (Extracción, Transformación y Carga) – ECOLUZ

#### Importación de librerías
###### Comandos de importación y breve explicación de las librerías utilizadas para manipulación, limpieza, transformación y modelado de datos.
```python
import pandas as pd                     # Manipulación y análisis de datos en DataFrames
import numpy as np                      # Cálculo numérico y operaciones con arrays
from math import pi                     # Soporte para gráficos polares y de radar

# Conexión con base de datos MongoDB
from dotenv import load_dotenv          # Carga de variables de entorno desde archivo .env
from pymongo import MongoClient         # Conexión y consultas a MongoDB

# Visualización
import matplotlib.pyplot as plt         # Gráficos estáticos
import seaborn as sns                   # Gráficos estadísticos estilizados

# Machine Learning y análisis
from sklearn.preprocessing import StandardScaler   # Escalado y normalización de datos
from sklearn.cluster import KMeans                 # Algoritmo de clustering K-Means
from sklearn.decomposition import PCA              # Reducción de dimensionalidad
from sklearn.metrics import silhouette_score       # Evaluación de calidad de clusters

# Estadística y utilidades
from scipy import stats                 # Funciones estadísticas adicionales
import os                               # Manejo de archivos y rutas
```

---

### Conexión y carga de datos desde MongoDB
###### Extracción de registros desde la colección `luminarias` en la base de datos MongoDB.
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

### Creación del DataFrame
###### Inspección inicial de los datos cargados en memoria.
```python
df.head()
df.info()
df.describe()
```

---

### Limpieza y transformación de datos
###### Procesos de depuración, estandarización y normalización.
```python
# Eliminación de nulos y duplicados
df_clean = df.drop_duplicates().dropna()

# Selección de columnas relevantes
features = ["name", "brand", "categories", "reviews.rating", "reviews.numHelpful"]

# Escalado numérico para clustering
scaler = StandardScaler()
df_scaled = scaler.fit_transform(df_clean[["reviews.rating", "reviews.numHelpful"]])
```

---

### Reducción de dimensionalidad (PCA)
###### Simplificación de variables manteniendo la varianza más representativa.
```python
pca = PCA(n_components=2)
df_pca = pca.fit_transform(df_scaled)
```

---

### Clustering con K-Means
###### Agrupamiento no supervisado de productos de Amazon en clusters.
```python
kmeans = KMeans(n_clusters=3, random_state=42)
df_clean["cluster"] = kmeans.fit_predict(df_pca)

# Evaluación con Silhouette Score
score = silhouette_score(df_pca, df_clean["cluster"])
print("Silhouette Score:", score)
```

---

### Visualización de datos (EDA + clustering)
###### Representación gráfica de distribución, correlaciones y clusters.
```python
plt.figure(figsize=(10,6))
sns.scatterplot(x=df_pca[:,0], y=df_pca[:,1], hue=df_clean["cluster"], palette="Set2")
plt.title("Clustering de productos - PCA + KMeans")
plt.show()
```

---

### Exportación del dataset limpio
###### Generación de archivos de salida para uso posterior.
```python
df_clean.to_csv("data/processed/amazon_clusters.csv", index=False)
```

---

### Conclusión de esta fase
La fase de **ETL y análisis no supervisado** permitió extraer datos desde MongoDB, transformarlos eliminando duplicados y valores nulos, escalar las variables numéricas y aplicar un modelo de clustering K-Means con validación mediante *Silhouette Score*.  

Como resultado, se obtuvo un dataset limpio y etiquetado con clusters, listo para análisis exploratorio, visualizaciones avanzadas y aplicaciones de segmentación de productos. 
