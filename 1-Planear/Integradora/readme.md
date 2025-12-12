#  Ecoluz Urbana – Prototipo de Aplicación Móvil Empresarial  
**Equipo: LAKID | UTXJ**

---

##  Identidad de Imagen  
### Logotipo de la Empresa  
<p align="center">
  <img src="assets/EUrbanalogo.png" alt="Icono de la Aplicación" width="150"/>
</p>


### Paleta de Colores  
- Primario: #1FA1AE
- Secundario: #0A67AC


### Tipografías  
- Títulos:  Inter-google font
- Cuerpo de texto:  Mulish-Google font

---

##  Descripción General del Prototipo  
Ecoluz Urbana es una plataforma inteligente diseñada para optimizar el monitoreo, gestión y mantenimiento del alumbrado público mediante tecnologías IoT, análisis de datos en tiempo real y herramientas digitales accesibles para administradores municipales, operadores y técnicos de campo.  
El sistema integra una **API REST**, un **dashboard administrativo web**, una **aplicación Wear OS**, el **prototipo de una aplicación móvil**, y sensores conectados que envían información sobre consumo, estado operativo y fallas.  

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
2. Procesar datos IoT y almacenar consumo energético.  
3. Integrar un dashboard web con mapas interactivos y gráficas.  
4. Implementar autenticación segura con JWT y roles.  
5. Crear un prototipo navegable en Figma y avances programados de la app.  
6. Proveer herramientas para técnicos mediante un wearable.

---

##  Organigrama del Equipo LAKID  

```
                 ┌─────────────────────────┐
                 │  Líder del Proyecto     │
                 │  Luis Iván Márquez A.   │
                 └─────────────┬───────────┘
                               │
        ┌──────────────────────┼─────────────────────────┐
        │                      │                         │
        ▼                      ▼                         ▼
┌───────────────┐     ┌────────────────┐        ┌───────────────────────┐
│    Backend     │     │    Frontend    │        │    Documentación      │
│ Kalid Reyes   │     │ Luis Iván M.A. │        │ Angel D. Reyes T.     │
│                │     │ Aldo T. D.     │        │                       │
└───────────────┘     └────────────────┘        └───────────────────────┘
```

---

##  Tabla de Roles  
| Integrante | Matrícula | Rol Principal | Responsabilidades |
|-----------|-----------|----------------|------------------|
| **Angel David Reyes Téllez** | 220432 | Documentación | API, PHVA, CI/CD, pruebas |
| **Brayn Kalid Reyes Silva** | 220244 | Backend | API, endpoints, base de datos |
| **Aldo Tolentino Domingo** | 220700 | Móvil / Frontend | App smartwatch, interfaz móvil |
| **Luis Iván Márquez Azuara** | 220401 | Líder / Frontend | Consumo de API, mapas, coordinación |

---

##  Diagrama de Gantt

| Actividad                                   | S1 | S2 | S3 | S4 | S5 | S6 | S7 | S8 | S9 | S10 | S11 | S12 | S13 | S14 |
|---------------------------------------------|----|----|----|----|----|----|----|----|----|-----|-----|-----|-----|-----|
| Análisis y levantamiento de requisitos      | ███ | ███ |    |    |    |    |    |    |    |     |     |     |     |     |
| Diseño UX (sketches, wireframes, mockups)   |    | ███ | ███ | ███ |    |    |    |    |    |     |     |     |     |     |
| Desarrollo API Backend                      |    |     | ███ | ███ | ███ | ███ | ███ |    |    |     |     |     |     |     |
| Desarrollo Dashboard Web                    |    |     |     |     | ███ | ███ | ███ | ███ | ███ |     |     |     |     |     |
| Desarrollo Wear OS / App Técnico            |    |     |     |     |     |     | ███ | ███ | ███ | ███ |     |     |     |     |
| Integración de Módulos                      |    |     |     |     |     |     |     | ███ | ███ | ███ |     |     |     |     |
| Pruebas (H)                                 |    |     |     |     |     |     |     |     | ███ | ███ | ███ |     |     |     |
| Verificación (V)                            |    |     |     |     |     |     |     |     |     |     | ███ | ███ |     |     |
| Correcciones finales                        |    |     |     |     |     |     |     |     |     |     |     | ███ | ███ |     |
| Presentación y entrega final                |    |     |     |     |     |     |     |     |     |     |     |     | ███ | ███ |

---

##  Requerimientos Funcionales  
1. Autenticación mediante JWT.  
2. Gestión de usuarios y roles.  
3. CRUD de luminarias.  
4. Visualización en mapa interactivo.  
5. Recepción de datos IoT.  
6. Consulta de estadísticas energéticas.  
7. Panel de alertas.  
8. Historial de mantenimiento.  
9. Filtrado por zona, fecha, estado.  
10. Consulta de luminarias vía Wear OS.

---

##  Requerimientos No Funcionales  
1. Tiempo de respuesta API < 500 ms.  
2. Dashboard con carga < 2 s.  
3. Disponibilidad ≥ 99 %.  
4. Seguridad TLS + JWT + OWASP.  
5. Compatibilidad con navegadores modernos + Wear OS 3+.

---

##  Historias de Usuario  
**HU-01 – Administrador**  
Como administrador quiero iniciar sesión para acceder al sistema.

**HU-02 – Operador**  
Como operador quiero visualizar luminarias en un mapa para conocer su estado.

**HU-03 – Técnico**  
Como técnico quiero ver luminarias cercanas desde el smartwatch para agilizar reparaciones.

*(Agregar más hasta llegar a 10)*

---

##  Sketches / Wireframes / Mockups  
[*Sketches*](https://www.figma.com/design/h80hDv7A0ptkayCYpxX1Cu/E.-Urbana?node-id=1-5)
[*Mockups8](https://www.figma.com/design/h80hDv7A0ptkayCYpxX1Cu/E.-Urbana?node-id=1-2)

---

##  Prototipo Navegacional  
[*(Figma)*](https://www.figma.com/design/h80hDv7A0ptkayCYpxX1Cu/E.-Urbana?node-id=1-4)

---

##  API – Repositorio y Documentación  
Repositorio API: https://github.com/eurbana-dev/Api_Eurbana  
Documentación Swagger: https://github.com/eurbana-dev/Api_Eurbana/tree/main/Swagger

---

##  Avances Programados  
- Dashboard React  
- API Node.js  
- Wear OS  

---

##  Presentación  
*(Insertar PDF o link)*

---

##  Conclusiones  
Ecoluz Urbana demuestra la viabilidad técnica de un sistema de monitoreo inteligente basado en IoT, integrando sensores, API, dashboard y wearable en un prototipo funcional. Las pruebas confirman que el sistema puede escalar, mantener estabilidad y mejorar la gestión del alumbrado público mediante información precisa y en tiempo real.

---

##  Integrantes – Equipo LAKID  
- 220432 — **Angel David Reyes Téllez**  
- 220244 — **Brayn Kalid Reyes Silva**  
- 220700 — **Aldo Tolentino Domingo**  
- 220401 — **Luis Iván Márquez Azuara**
