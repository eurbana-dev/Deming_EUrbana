# Procesos ETL — Ecoluz

Este directorio corresponde a la etapa **“Planear”** dentro del ciclo PHVA del proyecto *Ecoluz*.  
Aquí se documentan y prueban los procesos **ETL (Extract, Transform, Load)** aplicados a los datos de luminarias y registros de consumo energético.

---

## Estructura de carpetas

```
Deming_EUrbana/
 └── 1-Planear/
     └── ProcesosETL/
         ├── notebook_etl/
         │   └── etl_luminarias.ipynb   # Notebook principal con prototipo ETL
         └── readme.md                  # Documento contextual
```

- **`notebook_etl/`**: contiene un cuaderno Jupyter (`.ipynb`) con ejemplos prácticos de cómo se realizan las fases del ETL.  
- **`etl_luminarias.ipynb`**: prototipo que demuestra cómo leer datos masivos (CSV de luminarias), normalizar columnas, manejar tipos de datos y generar una salida limpia lista para ser consumida por la API o cargada en MongoDB.  
- **`readme.md`**: documento de referencia (este archivo), que explica la finalidad del directorio y cómo se conecta con el proyecto general.

---

## Propósito

Los procesos ETL son necesarios para:

1. **Extracción:** leer datos en bruto de archivos CSV (ej. inventario de luminarias de hasta 2 GB).  
2. **Transformación:** limpiar inconsistencias, convertir formatos de fecha, validar coordenadas GPS, estandarizar identificadores.  
3. **Carga:** enviar la información ya normalizada hacia la **API Ecoluz** o directamente a la **base de datos MongoDB**.

---

## Relación con el proyecto

- **API Seeder:** ambos módulos se complementan; el *seeder* inyecta datos en la API, mientras que los notebooks ETL definen cómo se preparan esos datos antes de insertarlos.  
- **Modelo del Sistema:** los procesos ETL aseguran que los datos lleguen en el formato esperado por la API y el panel web.  
- **Requisitos del Sistema:** responden a los requisitos de filtrado, limpieza de datos y optimización de consultas.  
- **Pruebas de la API:** la información cargada mediante ETL sirve para verificar el correcto funcionamiento de endpoints como `/api/luminarias`, `/api/consumo` y `/api/consumo/bulk`.

---

## Notas

- El notebook es un prototipo académico/documental.  
- No está pensado para producción, pero sirve como base para diseñar pipelines más robustos (Airflow, NiFi, etc.).  
- El ETL debe mantenerse actualizado si cambia la estructura del dataset o los requerimientos de la API.
