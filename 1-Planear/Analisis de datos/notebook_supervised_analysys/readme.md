# Propuesta de Aplicación

El equipo propone un sistema de análisis supervisado para el mantenimiento predictivo de luminarias urbanas. El objetivo es obtener predicciones sobre el estado de cada lámpara (bueno, regular, malo), realizar reducción de dimensionalidad para visualizar agrupamientos y analizar la importancia de variables que influyen en el deterioro. Se busca facilitar la toma de decisiones y optimizar recursos de mantenimiento.

# Elección del Mecanismo a Utilizar

Se seleccionó el algoritmo Random Forest para el análisis supervisado, debido a su robustez ante datos mixtos, capacidad de manejar variables numéricas y categóricas, y su utilidad para calcular la importancia de cada variable. Este mecanismo permite realizar predicciones, clasificaciones y recomendaciones basadas en principios matemáticos y estadísticos.

# Marco Teórico

El análisis supervisado utiliza algoritmos de aprendizaje automático que, a partir de datos etiquetados, aprenden patrones para predecir nuevas observaciones.  
Random Forest es un conjunto de árboles de decisión que se entrenan con subconjuntos aleatorios de datos y variables. La predicción final se obtiene por votación de los árboles.

Las métricas principales son:

- **Accuracy**: proporción de predicciones correctas.
- **Precision**: exactitud de las predicciones positivas.
- **Recall**: capacidad de encontrar todos los positivos reales.
- **F1-score**: media armónica entre precision y recall.

La reducción de dimensionalidad (PCA) permite visualizar los datos en 2D, facilitando la identificación de agrupamientos y la comprensión de la estructura interna del dataset.

# Aplicación del Mecanismo

Se aplicaron los siguientes comandos y pasos al dataset:

1. Limpieza de datos: eliminación de duplicados, nulos y outliers.
2. Ingeniería de features: creación de variables derivadas.
3. Selección y escalado de variables.
4. Entrenamiento y evaluación del modelo Random Forest.
5. Visualización de resultados y agrupamientos.

# Gráficos Generados

## 1. Importancia de Variables (Random Forest)

![Importancia de Variables](Importancia%20de%20variables.png)

Este gráfico horizontal muestra la importancia relativa de cada variable en el modelo Random Forest para predecir el estado de las luminarias. Generado en la celda de análisis de importancia de variables del notebook ECOLUZ_Analisis.ipynb, revela que:

- **Variables más influyentes**: `consumo.actual_watts`, `consumo.acumulado_kwh.mes`, `eficiencia.lumens_por_watt` y `consumo.acumulado_kwh.semana` tienen los scores más altos (≈0.08)
- **Variables moderadamente importantes**: `eficiencia.vida_util_restante_pct`, `eficiencia.horas_funcionamiento_total`, `sensores.luminosidad_lux` y `sensores.humedad_pct` 
- **Variables menos relevantes**: `potencia_watts` y `sensores.movimiento` muestran menor capacidad predictiva

La importancia se calcula mediante la reducción promedio de impureza que cada variable aporta a los árboles del bosque.

## 2. Matriz de Confusión

![Matriz de Confusión](Matriz%20de%20confusion.png)

Heatmap que visualiza el rendimiento del clasificador Random Forest, mostrando las predicciones vs. los valores reales. Generada en la celda de evaluación del modelo:

- **Diagonal principal**: Predicciones correctas por clase
  - Bueno: 150 predicciones correctas
  - Malo: 128 predicciones correctas  
  - Regular: 105 predicciones correctas
- **Elementos fuera de la diagonal**: Errores de clasificación
  - Mayor confusión entre estados "bueno" y "malo" (127 y 152 errores respectivamente)
  - El modelo tiene dificultades para distinguir claramente entre las tres categorías

El accuracy general del modelo es de aproximadamente 33%, indicando la necesidad de mejoras en las características o el algoritmo.

## 3. Visualización PCA de Luminarias

![Visualización PCA](Visualizacion%20PCA%20de%20luminarias.png)

Gráfico de dispersión en 2D resultado de aplicar Análisis de Componentes Principales (PCA) para reducir la dimensionalidad del dataset. Generado en la celda de visualización dimensional:

- **Ejes PC1 y PC2**: Primeros dos componentes principales que capturan la mayor varianza de los datos
- **Colores**: Representan el estado real de las luminarias según la escala mostrada (0.00 a 2.00)
- **Distribución**: No se observan clusters claramente separados, lo que explica el bajo rendimiento del modelo supervisado
- **Solapamiento**: Las diferentes clases se superponen significativamente en el espacio bidimensional

Esta visualización confirma que las variables actuales no permiten una separación clara entre los estados de las luminarias, sugiriendo la necesidad de ingeniería de características adicional.

# Resultados Obtenidos

El modelo logró un accuracy promedio del 33%, indicando que el estado de las luminarias es difícil de predecir con las variables actuales. La matriz de confusión muestra que las clases se confunden entre sí, y los gráficos de importancia de variables destacan factores como vida útil restante y horas de funcionamiento total. La visualización PCA revela que no existen agrupamientos claros, lo que explica el bajo desempeño del modelo.

# Conclusión de la Fase del Proyecto

Esta fase permitió estructurar y depurar el dataset, aplicar técnicas de análisis supervisado y visualizar los resultados. Aunque el modelo aún no logra una alta precisión, se identificaron variables clave y se sentaron las bases para futuras mejoras. La importancia de esta etapa radica en la generación de conocimiento y en la validación de los datos, fundamentales para la toma de decisiones y el desarrollo de soluciones inteligentes en