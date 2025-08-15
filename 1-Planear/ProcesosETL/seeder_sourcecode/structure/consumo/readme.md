# 📄 Documentación del Modelo `ModelConsumoSensor`

Este documento describe la estructura y el significado de cada campo del modelo **ConsumoSensor**, utilizado para almacenar registros de datos de sensores por minuto para cada luminaria en la base de datos MongoDB.

---

## 📌 Estructura del documento

class ModelConsumoSensor {
	constructor(
		_id,
		luminaria_id,
		timestamp,
		consumo,
		lumenes,
		encendida
	) {
		this._id = _id;
		this.luminaria_id = luminaria_id;
		this.timestamp = new Date(timestamp); 
		this.consumo = consumo; 
		this.lumenes = lumenes; 
		this.encendida = encendida; 
	}
}

module.exports = { ModelConsumoSensor };

---

## 📋 Campos del documento

| Campo            | Tipo      | Descripción |
|------------------|-----------|-------------|
| **_id**          | `string`  | Identificador único interno generado por MongoDB. |
| **luminaria_id** | `string`  | ID de la luminaria asociada al registro de consumo. |
| **timestamp**    | `Date`    | Fecha y hora exacta correspondiente al minuto del registro. |
| **consumo**      | `number`  | Consumo eléctrico en ese minuto (puede medirse en `Watts` o `kWh`). |
| **lumenes**      | `number`  | Cantidad de lúmenes generados en ese minuto. |
| **encendida**    | `boolean` | Estado de la luminaria en ese minuto (`true` = encendida, `false` = apagada). |

---

## 🗺 Ejemplo de documento 

{
    "_id": "64f8d1b2a1c34e789f123456",
    "luminaria_id": "64f7c1a2b9d13e456f789012",
    "timestamp": "2024-08-15T14:35:00.000Z",
    "consumo": 55.4,
    "lumenes": 1200,
    "encendida": true
}

---

## 🛠 Uso en el código

const { ModelConsumoSensor } = require('./ModelConsumoSensor');

const nuevoRegistro = new ModelConsumoSensor(
    null,
    '64f7c1a2b9d13e456f789012',
    '2024-08-15T14:35:00.000Z',
    55.4,
    1200,
    true
);

console.log(nuevoRegistro);
