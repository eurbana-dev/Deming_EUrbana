# ECOLUZ — MONITOREO INTELIGENTE DE LUMINARIAS PÚBLICAS

---

## Introducción
Ecoluz es un sistema de monitoreo para luminarias públicas que permite **detectar fallas**, **vigilar consumo** y **ubicar** cada punto de luz por **coordenadas GPS**. El proyecto integra:
- Una **API** para registrar/consultar el estado de las luminarias.
- Un **panel web** para administración, métricas y reportes.
- Un **wearable** para técnicos de campo que reciben alertas y confirman mantenimiento en sitio.

El objetivo es reducir tiempos de respuesta, mejorar la seguridad de las calles y optimizar el gasto energético municipal mediante analítica y automatización.

---

## Identidad Gráfica

![alt text](image.png)
<img width="200" height="200" alt="LAKID" src="https://github.com/user-attachments/assets/1ac23853-96fa-47a6-bdb6-ffa1669e0ff6" />

---

## Descripción
Ecoluz centraliza la telemetría de luminarias (estado on/off, consumo estimado, ubicación, fecha de último servicio), ejecuta **ETL** para limpiar y normalizar datos y aplica **análisis supervisado y no supervisado** para detectar anomalías y proponer **rutas de mantenimiento**. El sistema expone endpoints REST para integrar proveedores externos y generar reportes periódicos para la administración pública.

---

## Planteamiento del problema
Las ciudades enfrentan:
- Falta de **visibilidad en tiempo real** del estado de las luminarias.
- **Reportes ciudadanos dispersos** y sin trazabilidad.
- **Rutas de mantenimiento ineficientes**, que incrementan costos.
- Pérdidas por **consumo anómalo** y robo/falla de componentes.

Esto genera **calles oscuras**, percepción de inseguridad, y **sobre costo** de operación.

---

## Propuesta de solución
**Arquitectura funcional y técnica (resumen):**
- **Sensores/Dispositivos** por luminaria → envían telemetría (estado, tensión, consumo, GPS) a la **API**.
- **API** (Node/Express o Python/FastAPI) → valida, almacena y expone endpoints de consulta y administración.

- **Análisis**:
  - **Supervisado**: predicción de falla, clasificación de anomalías.
  - **No supervisado**: clustering de zonas con alta incidencia.
- **Panel Web** (React/Vite) → tablero, mapas, alertas, KPIs, exportables.
- **Wear OS** (Kotlin) → notificaciones, checklists y cierre de OT en campo.
- **Disponibilidad**: contenedores, orquestación de jobs, backups.

**Puntos significativos:**
- Disminución de **MTTR** (tiempo medio de reparación).
- Priorización de mantenimiento por **impacto y riesgo**.
- Transparencia con **evidencia** (OT cerradas con geolocalización/foto).

---

## Objetivo General
Desarrollar e implantar una plataforma integral que **monitoree, diagnostique y optimice** el mantenimiento de luminarias públicas, mejorando la seguridad y reduciendo costos operativos.

---

## Objetivos Específicos
1. Implementar una **API segura** para ingestión y consulta de telemetría.
2. Diseñar un **proceso ETL reproducible** para limpieza y calidad de datos.
3. Construir **modelos analíticos** (supervisado y no supervisado) para detectar fallas y segmentar zonas.
4. Desplegar un **panel web** con mapas, APIs y generación de reportes.
5. Entregar un **wearable** para técnicos con flujo de trabajo en campo.


---

## Organigrama de Trabajo
```mermaid
flowchart TB
    LUIS["Líder / Front-end (Luis)"]
    KALID["Back-end / API (Kalid)"]
    ALDO["Wear OS / Kotlin (Aldo)"]
    DAVID["Documentador (David)"]

    LUIS --> KALID
    LUIS --> ALDO
    LUIS --> DAVID
```


---

##  Tabla de Colaboradores

| Foto | Nombre completo | Rol principal | GitHub | Correo |
|---|---|---|---|---|
| <img src="https://avatars.githubusercontent.com/u/0?v=4" width="48"> | **Angel David Reyes Téllez** |   Documentación  | [@angelR003](https://github.com/usuario-github) | Seyersdolphin@outlook.com |
| <img src= "https://avatars.githubusercontent.com/u/141973599?v=4" width="48">  | **Luis Iván Márquez Azuara** | Frontend  | [@luisivmaraz ](https://github.com/luisivmaraz) | luisivmaraz03@gmail.com |
| <img src= "https://avatars.githubusercontent.com/u/115129477?v=4"  width="48"> | **Brayn Kalid Reyes Silva** | backend| [@KalidRs ](https://github.com/KalidRs) | brayn4krs@gmail.com |
| <img src= "https://avatars.githubusercontent.com/u/147024614?v=4"  width="48"> | **Aldo Tolentino Domingo** | Wear OS  | [@Aldotd12 ](https://github.com/Aldotd12) | tolentinodomingodiego@gmail.com |


---

## Diagrama de Gantt


```mermaid
gantt
    title Ecoluz — Cronograma (PHVA)
    dateFormat  YYYY-MM-DD
    axisFormat  %d-%b

    section P — Planear
    Modelado del sistema              :done,   p1, 2025-07-25, 2025-08-01
    Requisitos del sistema            :done,   p2, 2025-07-28, 2025-08-05

    section H — Hacer (Implementación)
    API REST (Node/Express + MongoDB) :active, h1, 2025-08-01, 2025-08-10
    Web Admin (React + Leaflet)       :        h2, 2025-08-05, 2025-08-10
    Wear OS (Kotlin + Retrofit)       :        h3, 2025-08-08, 2025-08-15

    section V — Verificar (Pruebas)
    Pruebas API + Evidencia           :        v1, 2025-08-16, 2025-08-17
    Demo y validación con requisitos  :        v2, 2025-08-18, 2025-08-17

    section A — Actuar (Mejoras)
    Ajustes finales y README          :        a1, 2025-08-20, 2025-08-19
    Entrega y retroalimentación       :        a2, 2025-08-22, 2025-08-19
```

---

##  Lista de Tecnologías

**Backend / API**
- **Node.js** + **Express**
- **MongoDB** + **Mongoose**
- **JWT** (autenticación y autorización)
- **Swagger /** (documentación de endpoints)
- **CORS** (seguridad)

**Base de Datos**
- **MongoDB Atlas** (gestión y hosting)
- Índices para consultas frecuentes
- Backups semanales

**Frontend Web (Administración)**
- **React** (con Vite)
- **React Router** (navegación)


**Wearable (Técnicos)**
- **Kotlin** · **Wear OS 3+**
- **Jetpack Compose for Wear OS**

---
## 1) Objetos de alto valor

```mermaid
flowchart TB
    E["Ecoluz"]
    E --> L["Luminarias: GPS • Estado • Consumo"]
    E --> API["API REST (Node/Express): JWT • Endpoints"]
    E --> WEB["Web Admin (React+Leaflet): Mapa • Alertas • Reportes"]
    E --> WEA["Wear OS (Kotlin): Alertas • Detalle"]
    E --> DB["MongoDB: Luminarias • Consumo • Usuarios"]
    E --> OPS["Operaciones: Detección • Historial • Estadísticas"]
```


## 2) Entidades Significativas (ER)

```mermaid
erDiagram
    LUMINARIA ||--o{ CONSUMO : registra
    LUMINARIA ||--o{ ALERTA : genera
    LUMINARIA ||--o{ MANTENIMIENTO : tiene
    USUARIO }o--o{ ROL : posee
    USUARIO ||--o{ MANTENIMIENTO : ejecuta

    LUMINARIA {
      string id
      string identificador
      string tipo
      float lat
      float lng
      date fecha_instalacion
      boolean activo
    }
    CONSUMO {
      string id
      string luminaria_id
      datetime timestamp
      float consumo
      int lumenes
      boolean encendida
    }
    ALERTA {
      string id
      string luminaria_id
      string severidad  "critica|media|baja"
      string tipo       "apagada|sobrecalentamiento|anomalia"
      datetime creada_en
      boolean atendida
    }
    MANTENIMIENTO {
      string id
      string luminaria_id
      string usuario_id
      datetime fecha
      string tipo
      string notas
    }
    USUARIO {
      string id
      string nombre
      string apellido
      string correo
      string telefono
    }
    ROL {
      string id
      string nombre "admin|operador|tecnico"
    }
```
---

## 3) Entidad por Objetos (Class Diagram)

```mermaid
classDiagram
    class Luminaria {
      +id: string
      +identificador: string
      +tipo: string
      +lat: float
      +lng: float
      +fechaInstalacion: Date
      +activo: boolean
    }

    class Consumo {
      +id: string
      +luminariaId: string
      +timestamp: Date
      +consumo: float
      +lumenes: int
      +encendida: boolean
    }

    class Alerta {
      +id: string
      +luminariaId: string
      +tipo: string
      +severidad: string
      +creadaEn: Date
      +atendida: boolean
    }

    class Usuario {
      +id: string
      +nombre: string
      +apellido: string
      +correo: string
      +telefono: string
    }

    class Rol {
      +id: string
      +nombre: string
    }

    class Mantenimiento {
      +id: string
      +luminariaId: string
      +usuarioId: string
      +fecha: Date
      +tipo: string
      +notas: string
    }

    Luminaria "1" --> "many" Consumo
    Luminaria "1" --> "many" Alerta
    Usuario "1" --> "many" Mantenimiento
    Luminaria "1" --> "many" Mantenimiento
    Usuario "many" --> "many" Rol
```

---

## 4) Dominio del Proceso (Sequence)

```mermaid
sequenceDiagram
    autonumber
    participant Sensor as Sensor/Luminaria
    participant API as API REST (Node)
    participant DB as MongoDB
    participant Web as Web Admin (React)
    participant Wear as Wear OS (Kotlin)

    Sensor->>API: POST /consumo {luminaria, consumo, lumenes, encendida}
    API->>DB: Insert registro consumo
    DB-->>API: OK (id)
    API-->>Sensor: 201 Created

    API->>DB: Evaluar regla -> ¿falla?
    DB-->>API: Resultado (true/false)
    alt Falla detectada
        API->>DB: Insert ALERTA {luminaria, tipo, severidad}
        API-->>Web: WS/Event: nueva alerta
        API-->>Wear: Notificación: alerta en campo
    end

    Web->>API: GET /luminarias, /alertas
    API->>DB: Query
    DB-->>API: Datos
    API-->>Web: JSON (mapa, panel)
```

---

## 5) Modelo ADL Negocio (Flowchart)

```mermaid
flowchart TB
    subgraph Ciudadanía
      C1["Habitantes"]
    end

    subgraph Municipio
      M1["Admin Municipal"]
      M2["Técnicos de Mantenimiento"]
    end

    subgraph Ecoluz Plataforma
      W["Web Admin (decisiones)"]
      R["Reportes/Estadísticas"]
      A["API REST"]
      D["DB (Mongo)"]
      S["Sensores/Luminarias"]
      WEAR["Wear OS (campo)"]
    end

    C1 -->|Reporte de falla| M1
    M1 -->|Gestiona| W
    W -->|Solicitud datos| A --> D
    S -->|Telemetría| A
    A --> WEAR
    WEAR -->|Cierra alerta| A
    A --> R
    R --> M1
    M2 --> WEAR
```

---

## 6) Arquitectura de Capas (Flowchart con subgraphs)

```mermaid
flowchart TB
    subgraph Presentacion
      Web["Web Admin (React + Leaflet)"]
      Wear["Wear OS (Kotlin/Compose)"]
    end

    subgraph Aplicacion
      API["API REST (Express)"]
      Auth["Auth JWT"]
    end

    subgraph Dominio
      DomSrv["Servicios de Dominio"]
      Reglas["Reglas de alerta/negocio"]
    end

    subgraph Infraestructura
      DB[(MongoDB)]
      Logs["Winston/Morgan"]
      CI["GitHub Actions"]
      Maps["Mapas/Geocodificación"]
    end

    Web --> API
    Wear --> API
    API --> Auth
    API --> DomSrv
    DomSrv --> Reglas
    DomSrv --> DB
    API --> Logs
    API --> CI
    Web --> Maps
```

---

## 7) Arquitectura de la Solución (Flow/Data)

```mermaid
flowchart LR
    Sensors["Luminarias/Sensores"] --> Ingest["API /consumo (HTTP/JSON)"]
    Ingest --> Proc["Validación + Normalización"]
    Proc --> Rule["Motor de reglas (falla/umbral)"]
    Rule -->|falla| Alerts["/alertas (crear)"]
    Proc --> Store[(MongoDB)]
    Alerts --> NotifyWeb["Web Admin: WS/Event/Pooling"]
    Alerts --> NotifyWear["Wear OS: Notificación"]
    Web["React + Leaflet"] --> API["API REST"]
    Wear["Kotlin/Compose"] --> API
    API --> Store
    Web <---> Maps["Leaflet/TileServer"]
```

---
