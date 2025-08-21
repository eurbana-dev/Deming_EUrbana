# Documentación del Modelo ModelUsuario

Este documento describe la estructura y el significado de cada campo del modelo *Usuario*, utilizado para almacenar la información general de los usuarios en la base de datos **MongoDB**.

---

## Estructura del documento

```javascript
class ModelUsuario {
  constructor(
    _id,
    identificador,
    nombre,
    apellido,
    telefono,
    correo,
    contrasena,
    rol 
  ) {
    this._id = _id;
    this.identificador = identificador;
    this.nombre = nombre;
    this.apellido = apellido;
    this.telefono = telefono;
    this.correo = correo;
    this.contrasena = contrasena; 
    this.rol = rol;
  }
}

module.exports = { ModelUsuario };
```

---

## Campos del documento

| Campo           | Tipo    | Descripción |
|-----------------|---------|-------------|
| *_id*           | string  | Identificador único interno generado por MongoDB. |
| *identificador* | string  | Código único del usuario para consultas rápidas. |
| *nombre*        | string  | Nombre del usuario. |
| *apellido*      | string  | Apellido del usuario. |
| *telefono*      | string  | Número de teléfono de contacto. |
| *correo*        | string  | Dirección de correo electrónico. |
| *contrasena*    | string  | Contraseña cifrada del usuario. |
| *rol*           | string  | Rol asignado al usuario (`admin`, `supervisor`, `usuario`). |

---

## Ejemplo de documento

```json
{
  "_id": "64f7c1a2b9d13e456f789abc",
  "identificador": "USR-001",
  "nombre": "Juan",
  "apellido": "Pérez",
  "telefono": "+52 555-123-4567",
  "correo": "juan.perez@example.com",
  "contrasena": "$2b$10$abc123hashseguro",
  "rol": "admin"
}
```

---

## Uso en el código

```javascript
const { ModelUsuario } = require('./ModelUsuario');

const nuevoUsuario = new ModelUsuario(
  null,
  'USR-002',
  'María',
  'López',
  '+52 999-555-7890',
  'maria.lopez@example.com',
  'contraseñaCifrada123',
  'supervisor'
);

console.log(nuevoUsuario);
```
