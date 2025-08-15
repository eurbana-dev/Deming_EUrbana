# 📄 Documentación del Modelo `ModelLuminaria`

Este documento describe la estructura y el significado de cada campo del modelo **Luminaria**, utilizado para almacenar información sobre luminarias en la base de datos MongoDB.

---

## 📌 Estructura del documento

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

## 📋 Campos del documento

| Campo               | Tipo      | Descripción |
|---------------------|-----------|-------------|
| **_id**             | `string`  | Identificador único interno generado por MongoDB. |
| **identificador**   | `string`  | Código o ID físico visible de la luminaria en campo. |
| **tipo_luminaria**  | `string`  | Tipo de luminaria (ej. `LED`, `Solar`, `Halógena`). |
| **pais**            | `string`  | País donde se encuentra la luminaria. |
| **estado**          | `string`  | Estado o provincia donde se encuentra instalada. |
| **ciudad**          | `string`  | Ciudad en la que está ubicada. |
| **region**          | `string`  | Región geográfica específica (opcional). |
| **coordenadas**     | `object`  | Objeto con latitud y longitud de la ubicación exacta. |
| ├──> **lat**         | `number`  | Latitud geográfica. |
| └──> **lng**         | `number`  | Longitud geográfica. |
| **fecha_instalacion** | `Date`  | Fecha en que fue instalada la luminaria. |
| **activo**          | `boolean` | Estado operativo de la luminaria (`true` = activa, `false` = fuera de servicio). |

---

## 🗺 Ejemplo de documento en MongoDB

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

## 🛠 Uso en el código

```javascript
const { ModelLuminaria } = require('./ModelLuminaria');

const nuevaLuminaria = new ModelLuminaria(
    null,
    'LMN-002',
    'Solar',
    'México',
    'Yucatán',
    'Mérida',
    '6',
    { lat: 20.967370, lng: -89.592586 },
    '2024-02-10',
    true
);

