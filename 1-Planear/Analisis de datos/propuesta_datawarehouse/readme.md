# 🏙 Data Warehouse - E. Urbana

## 📌 Propuesta de Data Warehouse

El **Data Warehouse** de **E. Urbana** está diseñado para organizar y analizar información relacionada con el consumo y estado de luminarias en diferentes ubicaciones geográficas.  
Este sistema servirá como repositorio histórico y analítico que integra datos provenientes de múltiples fuentes internas y externas, facilitando la toma de decisiones estratégicas sobre el mantenimiento, optimización y gestión energética.

---

## 🌐 Contexto en el Proyecto

En el marco de **E. Urbana**, el objetivo principal es ofrecer soluciones inteligentes de gestión de luminarias que permitan reducir costos energéticos y optimizar el alumbrado público y privado.  
El Data Warehouse será un componente clave para:

- Consolidar datos históricos de **consumo energético** y **estado operativo** de cada luminaria.
- Permitir **consultas analíticas** y generación de reportes para la gestión técnica y financiera.
- Servir como base para modelos de **predicción de fallas** y **recomendación de consumo óptimo**.

---

## 📖 Características principales

- **Integración:** unifica datos de distintas fuentes.
- **Historización:** guarda versiones históricas para análisis temporal.
- **Consulta optimizada:** enfocado en análisis y no en transacciones.
- **Consistencia:** garantiza calidad y homogeneidad de la información.

---

## 🔍 Orígenes de Datos

El Data Warehouse de **E. Urbana** integrará información desde distintas fuentes:

1. **Base de datos operacional (MongoDB)**  
   Contiene la información detallada de cada luminaria y sus registros de consumo energético.

2. **Sensores IoT**  
   Datos en tiempo real sobre **consumo energético**, **estado operativo** y **fallas detectadas** Mediante la API.

3. **APIs externas**  
   Información complementaria como tarifas eléctricas o condiciones climáticas. (No contemplada para el MVP)

4. **Registros históricos**  
   Datos previos desde la implementación, extraidas de archivos csv para el analisis.

---

## 📊 Modelos de Machine Learning Integrados

### 🔹 Modelo Supervisado
- **Algoritmo:** KNN (*K-Nearest Neighbors*).
- **Objetivo:** Predecir fallas en luminarias a partir del patrón de consumo energético histórico y otros factores como ubicación y tipo de luminaria.
- **Datos de entrenamiento:** Historial de consumo energético y registros de fallas.
- **Uso en producción:** Alertar al equipo de mantenimiento antes de que ocurra una falla.

### 🔹 Modelo No Supervisado
- **Algoritmo:** K-Means (Clustering).
- **Objetivo:** Segmentar luminarias en grupos según patrones de consumo, para detectar anomalías, optimizar uso energético y recomendar configuraciones.
- **Datos de entrada:** Consumo histórico agregado por hora, día o mes.

---

## 📄 Modelo de Datos: `ModelLuminaria`

```javascript
class ModelLuminaria {
    constructor(
        _id, 
        identificador,
        tipo_luminaria,
        pais,
        estado,
        ciudad,
        region,
        coordenadas,
        fecha_instalacion,
        activo
    ) {
        this._id = _id;
        this.identificador = identificador;
        this.tipo_luminaria = tipo_luminaria;
        this.estado = estado;
        this.ciudad = ciudad;
        this.region = region;
        this.activo = activo;
        this.pais = pais;
        this.coordenadas = {
            lat: coordenadas.lat,
            lng: coordenadas.lng
        };
        this.fecha_instalacion = new Date(fecha_instalacion);
    }
}
```

---

### 📋 Campos del Modelo

| Campo               | Tipo      | Descripción |
|---------------------|-----------|-------------|
| **_id**             | `string`  | Identificador único generado por MongoDB. |
| **identificador**   | `string`  | Código o ID físico visible de la luminaria. |
| **tipo_luminaria**  | `string`  | Tipo de luminaria (`LED`, `Solar`, `Halógena`). |
| **pais**            | `string`  | País de ubicación. |
| **estado**          | `string`  | Estado o provincia. |
| **ciudad**          | `string`  | Ciudad de instalación. |
| **region**          | `string`  | Región geográfica específica. |
| **coordenadas**     | `object`  | Latitud y longitud. |
| ├──> **lat**        | `number`  | Latitud. |
| └──> **lng**        | `number`  | Longitud. |
| **fecha_instalacion** | `Date`  | Fecha de instalación. |
| **activo**          | `boolean` | Estado operativo (`true`/`false`). |

---

## 🗺 Ejemplo de Registro

```json
{
    "_id": "64f7c1a2b9d13e456f789012",
    "identificador": "LMN-001",
    "tipo_luminaria": "LED",
    "pais": "México",
    "estado": "Jalisco",
    "ciudad": "Guadalajara",
    "region": "4",
    "coordenadas": {
        "lat": 20.659698,
        "lng": -103.349609
    },
    "fecha_instalacion": "2023-05-15T00:00:00.000Z",
    "activo": true
}
```

---

## 📌 Próximos pasos

1. **Diseñar el modelo dimensional** (Esquema estrella) para el Data Warehouse. (En desarrollo)
2. **Implementar ETL** para extraer datos desde MongoDB y procesarlos para el Data Warehouse. (En desarrollo)
3. **Entrenar y validar** el modelo KNN para predicción de fallas. (Aun no)
4. **Implementar clustering** para análisis no supervisado de consumo. (Aun no)
5. **Desarrollar dashboards** interactivos para visualización de resultados. (En desarrollo)

---
