# API Seeder — Ecoluz (Node.js)

Monitoreo inteligente de luminarias públicas: utilidades para cargar datos masivos (luminarias y telemetría de consumo) hacia la API Ecoluz.

**Repositorio de la API:** [https://github.com/eurbana-dev/Api_Eurbana](https://github.com/eurbana-dev/Api_Eurbana)  
**Dataset (CSV):** [luminarias.csv (≈1.6 GB)](https://www.mediafire.com/file/dzz7s2yuaeu17gm/luminarias.csv/file)

---

## Objetivo

Este proyecto permite importar, en lotes, información de:

- Inventario de luminarias (identificador, tipo, ubicación, fechas, activo).  
- Registros de sensores (consumo, lúmenes, estado) para histórico y analítica.

La siembra usa carga por lotes para aprovechar el endpoint `/api/consumo/bulk` y minimizar latencia y overhead de múltiples peticiones.

---

## Arquitectura (resumen)

- **API:** Node.js + Express  
- **Base de datos:** MongoDB  
- **Frontend web:** React + Leaflet (mapas)  
- **Wear OS:** Kotlin (en progreso)

Funciones de la API utilizadas por este seeder:

- `POST /api/consumo/bulk` — inserción masiva de registros de sensores.  
- `POST /api/consumo` — inserción individual (fallback).  
- `GET /api/luminarias` — verificación y consulta de luminarias.  
- (Opcional) `POST /api/auth/login` — obtener token JWT si la API está protegida.

---

## Requisitos

- Node.js 18+ y npm  
- Acceso a la API Ecoluz en ejecución (local o remoto)  
- MongoDB accesible por la API  
- Token JWT válido (si las rutas están protegidas)

---

## Variables de entorno

Crear un archivo `.env` en la raíz del seeder:

```bash
API_BASE_URL=http://localhost:3000
JWT_TOKEN=eyJhbGciOi...   # Opcional si la API exige autenticación
BULK_SIZE=1000            # Registros por lote (ajustar según el entorno)
CSV_PATH=./data/luminarias.csv
```

> La API por defecto corre en `http://localhost:3000` y documenta sus rutas en `/api-docs`.

---

## Estructura esperada de los CSV

### 1. luminarias.csv (inventario)

Encabezados sugeridos:

```
identificador,tipo_luminaria,pais,estado,ciudad,region,lat,lng,fecha_instalacion,activo
LUM-001-MTY,LED,México,Nuevo León,Monterrey,Centro,25.6866,-100.3161,2023-01-15,true
```

Estos campos reflejan lo que expone la API al listar luminarias activas.

---

### 2. consumo.csv (opcional para telemetría)

```
luminaria_id,timestamp,consumo,lumenes,encendida
507f1f77bcf86cd799439012,2024-01-15T20:30:00.000Z,85.5,3200,true
```

Compatible con `/api/consumo` y `/api/consumo/bulk`.  
Para estadísticas: `/api/consumo/estadisticas/{luminaria_id}`.

---

## Instalación

```bash
git clone https://github.com/eurbana-dev/Api_Eurbana
# (opcional) si el seeder está en otro repositorio, clónalo y entra a su carpeta
npm install
```

---

## Uso básico

### 1. Seed de inventario de luminarias (modo “dry-run”)

```bash
node scripts/seed-luminarias.js --csv ./data/luminarias.csv --dry-run
```

Valida columnas, coordenadas y fechas sin enviar datos a la API.

---

### 2. Seed real de luminarias

```bash
node scripts/seed-luminarias.js --csv ./data/luminarias.csv
```

Inserta o actualiza luminarias (upsert por identificador).

---

### 3. Seed de telemetría por lotes

```bash
node scripts/seed-consumo-bulk.js --csv ./data/consumo.csv --bulk 1000
```

Envía lotes a `POST /api/consumo/bulk` con tamaño configurable.

---

## Rendimiento y manejo de archivos grandes (≈2 GB)

- Lectura en **streaming** (`fs.createReadStream` + `readline`/`csv-parse`) para no cargar todo en memoria.  
- **Particionado previo**: dividir CSV en fragmentos de 200–500 MB en equipos con pocos recursos.  
- `BULK_SIZE` recomendado: 500–2000 registros (ajustar si ocurren timeouts).  
- **Índices en MongoDB**: crear índices sobre `luminaria_id` y `timestamp`.  
- **Mantenimiento de datos**: usar `DELETE /api/consumo/limpieza/antiguos?fecha_limite=...` para limpiar históricos.

---

## Autenticación


1. Obtener token con `POST /api/auth/login` (correo + contraseña).  
2. Exportar `JWT_TOKEN` en el entorno o pasarlo por CLI.  
3. El seeder usará el encabezado:  

```
Authorization: Bearer <TOKEN>
```

---

## Verificación rápida (post-seed)

- `GET /api/luminarias` → listar luminarias activas.  
- `GET /api/consumo?limite=20` → registros recientes de consumo.  
