# 📄 Documentación del Modelo ModelMantenimiento

Este documento describe la estructura y el significado de cada campo del modelo *Mantenimiento*, utilizado para almacenar información sobre los mantenimientos realizados a luminarias en la base de datos MongoDB.

---

## 📌 Estructura del documento

```javascript
class ModelMantenimiento {
    constructor(
        _id,
        luminaria_id,
        responsable_id,
        fecha,
        id_mantenimiento_anterior,
        estatus,
        observaciones,
        tipo_mantenimiento
    ) {
        this._id = _id;
        this.luminaria_id = luminaria_id;
        this.responsable_id = responsable_id;
        this.fecha = new Date(fecha);
        this.id_mantenimiento_anterior = id_mantenimiento_anterior;
        this.estatus = estatus;
        this.observaciones = observaciones;
        this.tipo_mantenimiento = tipo_mantenimiento;
    }
}
```

---

## 📋 Campos del documento

| Campo                      | Tipo    | Descripción                                                                 |
|----------------------------|---------|-----------------------------------------------------------------------------|
| *_id*                      | string  | Identificador único interno generado por MongoDB para el mantenimiento.     |
| *luminaria_id*             | string  | ID de la luminaria asociada al mantenimiento.                               |
| *responsable_id*           | string  | ID del responsable que realizó o supervisó el mantenimiento.                |
| *fecha*                    | Date    | Fecha en la que se realizó el mantenimiento.                                |
| *id_mantenimiento_anterior*| string  | ID del mantenimiento previo, si existe (para historial encadenado).         |
| *estatus*                  | string  | Estado del mantenimiento (`pendiente`, `completado`, `en proceso`).         |
| *observaciones*            | string  | Comentarios o detalles adicionales sobre el mantenimiento realizado.         |
| *tipo_mantenimiento*       | string  | Tipo de mantenimiento (`preventivo`, `correctivo`).                         |

---

## 🗺 Ejemplo de documento 

```json
{
    "_id": "64f8d2a3b9d13e456f789999",
    "luminaria_id": "64f7c1a2b9d13e456f789012",
    "responsable_id": "USR-001",
    "fecha": "2024-07-10T00:00:00.000Z",
    "id_mantenimiento_anterior": "64f8c5b2b9d13e456f789888",
    "estatus": "completado",
    "observaciones": "Cambio de lámpara LED y revisión del sistema eléctrico.",
    "tipo_mantenimiento": "correctivo"
}
```

---

## 🛠 Uso en el código

```javascript
const { ModelMantenimiento } = require('./ModelMantenimiento');

const nuevoMantenimiento = new ModelMantenimiento(
    null,                                 // _id (MongoDB lo genera)
    "64f7c1a2b9d13e456f789012",           // luminaria_id
    "USR-002",                            // responsable_id
    "2024-08-01",                         // fecha
    null,                                 // id_mantenimiento_anterior
    "pendiente",                          // estatus
    "Revisión programada de luminaria en zona norte", // observaciones
    "preventivo"                          // tipo_mantenimiento
);

console.log(nuevoMantenimiento);
```