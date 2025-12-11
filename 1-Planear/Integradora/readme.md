#  Ecoluz Urbana – Prototipo de Aplicación Móvil Empresarial  
**Equipo: LAKID | UTXJ ***

---

##  Identidad de Imagen  
### Logotipo de la Empresa  
> *(Insertar imagen)*  

### Logotipo del Producto  
> *(Insertar imagen)*  

### Paleta de Colores  
- Primario: #  
- Secundario: #  
- Acento: #  
> *(Insertar imagen)*  

### Tipografías  
- Títulos:  
- Cuerpo de texto:  

---

##  Descripción General del Prototipo (150–300 palabras)  
Ecoluz Urbana es una plataforma inteligente diseñada para optimizar el monitoreo, gestión y mantenimiento del alumbrado público mediante tecnologías IoT, análisis de datos en tiempo real y herramientas digitales accesibles para administradores municipales, operadores y técnicos de campo.  
El sistema integra una **API REST**, un **dashboard administrativo web**, una aplicación **Wear OS** para técnicos, el prototipado de una aplicacion movil y sensores conectados que envían información sobre consumo, estado operativo y fallas.  
El prototipo aborda problemáticas comunes como luminarias fuera de servicio, falta de información precisa, altos costos operativos y ausencia de herramientas de monitoreo centralizado.

Con Ecoluz Urbana, las instituciones pueden:  
- Visualizar el estado y ubicación de luminarias en mapas interactivos.  
- Analizar consumos energéticos con gráficas en tiempo real.  
- Recibir alertas de fallas y planificar mantenimientos.  
- Registrar información desde campo mediante smartwatch.  

El objetivo del prototipo es demostrar la viabilidad funcional y técnica de un sistema unificado que reduzca costos, mejore la eficiencia energética y aumente la seguridad ciudadana.

---

##  Objetivo General  
Implementar un prototipo funcional de monitoreo inteligente de luminarias capaz de centralizar información operativa y energética, facilitando la toma de decisiones y el control municipal.

---

##  Objetivos Específicos  
1. Visualizar el estado operativo de luminarias en tiempo real.  
2. Procesar datos IoT y almacenar consumo energético en la base de datos.  
3. Integrar un dashboard web con mapas interactivos y gráficas.  
4. Implementar autenticación segura mediante JWT y roles.  
5. Crear un prototipo navegable en Figma y avances programados de la app.  
6. Proveer herramientas para técnicos mediante wearable.  

---

##  Organigrama del Equipo LAKID  

- Líder del Proyecto  
- Backend  
- Frontend  
- UX/UI  
- Documentación  Luis Iván Márquez Azuara  
        │  
        ├── Líder del Proyecto
        │
        ├── Khalid Reyes Silva ─── Backend
        │
        ├── Área Frontend
        │        ├── Luis Iván Márquez A.  
        │        └── Aldo Tolentino Domingo
        │
        └── Documentación  
                 └── Angel David Reyes Téllez


---

## Tabla de Roles  
| Integrante | Matrícula | Rol Principal | Responsabilidades |
|-----------|-----------|----------------|------------------|
| **Angel David Reyes Téllez** | 220432 |  Documentación | API, PHVA, CI/CD, pruebas |
| **Brayan Khalid Reyes Silva** | 220244 | Backend | Api, mapas, integración UI |
| **Aldo Tolentino Domingo** | 220700 | Móvil / Frontend | App smartwatch, lógica de consumo |
| **Luis Iván Márquez Azuara** | 220401 | Lider / FrontEnd | Consumo API Mapas |

---

## Diagrama de Gantt (Cronograma)

| Actividad                                   | Semana 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 |
|---------------------------------------------|----------|---|---|---|---|---|---|---|---|----|----|----|----|----|
| Análisis y levantamiento de requisitos      | ████████ | ████████ |   |   |   |   |   |   |   |    |    |    |    |    |
| Diseño UX (sketches, wireframes, mockups)   |          | ████████ | ████████ | ████████ |   |   |   |   |   |    |    |    |    |    |
| Desarrollo API Backend (Node.js + MongoDB)  |          |         | ████████ | ████████ | ████████ | ████████ | ████████ |   |   |    |    |    |    |    |
| Desarrollo Dashboard Web (React/Vue)        |          |         |         |         | ████████ | ████████ | ████████ | ████████ | ████████ |    |    |    |    |    |
| Desarrollo Wear OS / App Técnico            |          |         |         |         |         |         | ████████ | ████████ | ████████ | ████████ |    |    |    |    |
| Integración de Módulos                      |          |         |         |         |         |         |         | ████████ | ████████ | ████████ |    |    |    |    |
| Pruebas (H)                                 |          |         |         |         |         |         |         |         | ████████ | ████████ | ████████ |    |    |    |
| Verificación (V)                            |          |         |         |         |         |         |         |         |         |         | ████████ | ████████ |    |    |
| Correcciones finales / Ajustes              |          |         |         |         |         |         |         |         |         |         |         | ████████ | ████████ |    |
| Presentación y entrega final                |          |         |         |         |         |         |         |         |         |         |         |         | ████████ | ████████ |


---

##  Requerimientos Funcionales  
1. Autenticación mediante JWT.  
2. Gestión de usuarios y roles.  
3. CRUD de luminarias.  
4. Visualización en mapa interactivo.  
5. Recepción de datos IoT (consumo, lúmenes, estado).  
6. Consulta de estadísticas energéticas.  
7. Panel de alertas por fallas.  
8. Historial de mantenimiento.  
9. Filtrado por zona, fecha, estado.  
10. Consulta de luminarias desde Wear OS.  

---

##  Requerimientos No Funcionales  
1. Tiempo de respuesta API < 500 ms.  
2. Dashboard con carga < 2 s.  
3. Disponibilidad ≥ 99 %.  
4. Seguridad TLS + JWT + OWASP.  
5. Compatibilidad: Chrome, Firefox, Edge; Wear OS 3+.  

---

##  Historias de Usuario  
**HU-01 – Administrador**  
*Como administrador quiero iniciar sesión para acceder al sistema de monitoreo.*  

**HU-02 – Operador**  
*Como operador quiero ver las luminarias en el mapa para identificar el estado de cada una.*  

**HU-03 – Técnico de campo**  
*Como técnico quiero consultar las luminarias cercanas desde el smartwatch para agilizar reparaciones.*  

*(Agregar más hasta completar mínimo 10)*

---

##  Sketches  
> *(Insertar imagen o link Figma)*  

##  Wireframes  
> *(Insertar imagen o link Figma)*  

##  Mockups  
> *(Insertar imagen o link Figma)*  

##  Prototipo Navegacional  
> *(Insertar link de Figma)*  

---

##  API – Repositorio y Documentación  
Repositorio API: 
Documentación Swagger: *(Insertar link)*  

---

## Prototipo Programado (Avances)  
- Dashboard React: *(link a repo o deploy)*  
- API Node.js: *(repo / deploy)*  
- Wear OS: *(repo o capturas)*  

---

##  Presentación  
> *(Insertar)*  

---

##  Conclusiones  
Ecoluz Urbana demuestra la viabilidad técnica de un sistema de monitoreo inteligente basado en IoT, logrando integrar sensores, API, dashboard y wearable en un prototipo funcional.  
Las pruebas indican que el sistema puede escalar, ofrece tiempos de respuesta adecuados y mejora la gestión del alumbrado público mediante información precisa y en tiempo real.  

---

##  Integrantes – Equipo LAKID  
- 220432 — **Angel David Reyes Téllez**  
- 220244 — **Brayan Khalid Reyes Silva**  
- 220700 — **Aldo Tolentino Domingo**  
- 220401 — **Luis Iván Márquez Azuara**
