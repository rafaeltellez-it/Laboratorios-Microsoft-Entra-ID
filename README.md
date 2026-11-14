# 🛡️ Portafolio Práctico: Administración de Identidades (Microsoft Entra ID / SC-300) y Soporte TI

¡Hola! Soy **Ronald Rafael Tellez**, especialista en **Soporte Técnico TI (Helpdesk Tier 1/2)** y en formación para **Administración de Identidades y Accesos (IAM)** con enfoque en tecnologías Microsoft y redes Cisco.

Este repositorio documenta mi **laboratorio práctico empresarial (Homelab)** en **Microsoft Entra ID (Azure AD)**. Aquí resuelvo escenarios reales basados en tickets de soporte, requerimientos de seguridad corporativa y cumplimiento de acuerdos de nivel de servicio (**SLA**).

---

## 🛠️ Tecnologías y Herramientas Aplicadas
* **Identidad y Nube:** Microsoft Entra ID (Free & P2), Azure Portal, Microsoft 365 Admin Center.
* **Seguridad y Accesos:** Acceso Condicional (Conditional Access), Autenticación Multifactor (MFA), Autoservicio de restablecimiento de contraseñas (SSPR), Control de acceso basado en roles (RBAC).
* **Soporte y Diagnóstico:** Análisis de Sign-in Logs y Audit Logs, resolución de problemas de inicio de sesión, gestión de incidencias bajo métricas SLA (Jira / Service Desk).
* **Infraestructura Base:** Cisco IT Essentials, Redes TCP/IP, Diagnóstico OSI Nivel 1-3, Windows 10/11 Pro.

---

## 📋 Índice de Tickets y Laboratorios Resueltos

| # Ticket | Escenario / Incidencia | Herramienta en Entra ID | Prioridad / SLA | Estado |
| :--- | :--- | :--- | :--- | :--- |
| **INC-001** | Incorporación masiva de empleados y asignación de grupos por departamento | Usuarios / Grupos Dinámicos / CSV | Media (4 hrs) | ✅ Resuelto |
| **INC-002** | Usuario bloqueado y habilitación de restablecimiento de contraseña (SSPR) | Password Reset / Authentication Methods | Alta (1 hr) | ✅ Resuelto |
| **REQ-003** | Exigir MFA obligatorio al área de Finanzas y bloquear accesos fuera del país | Conditional Access / Named Locations | Alta (2 hrs) | ✅ Resuelto |
| **INC-004** | Diagnóstico de error de inicio de sesión mediante registros de auditoría | Sign-in Logs / Troubleshooting | Crítica (30 min) | ✅ Resuelto |

---

# 🎫 Ticket INC-001: Incorporación de personal y automatización de grupos

* **Solicitante:** Recursos Humanos (RRHH)
* **Prioridad:** Media (SLA: 4 horas)
* **Categoría:** Administración de Identidades (IAM) - Microsoft Entra ID

### 1. Descripción del Problema / Requerimiento
RRHH solicita dar de alta a nuevos ingresos del área de Ventas y Soporte Técnico. Se requiere que las licencias y permisos se asignen automáticamente según su departamento sin intervención manual futura.

### 2. Procedimiento Técnico Ejecutado
1. **Importación Masiva (Bulk Create):** Se descargó y completó la plantilla `.csv` de Microsoft Entra ID con los atributos `userPrincipalName`, `department`, `jobTitle` y `usageLocation`.
2. **Creación de Grupo Dinámico:** Se creó el grupo de seguridad `GRP-Departamento-Ventas` configurando el tipo de membresía en **Usuario Dinámico**.
3. **Regla de Membresía Dinámica:** Se configuró la expresión `(user.department -eq "Ventas")` para automatizar la asignación.

<img width="1913" height="806" alt="usuario-carlos" src="https://github.com/user-attachments/assets/09f0cc63-ac6f-48e3-b0d7-2374332c2760" />

<img width="1920" height="921" alt="grupo-ventas" src="https://github.com/user-attachments/assets/d1150c5a-88e8-4101-953c-f3aa79318f1c" />


### 3. Verificación y Pruebas
* Se validó en la pestaña **Bulk operation results** que los usuarios fueron creados sin errores (100% completado).
* Se verificó que el grupo dinámico procesó la regla y agregó automáticamente a los usuarios correspondientes.

### 4. Respuesta de Cierre del Ticket (Notificación al Usuario)
> "Estimado equipo de RRHH: Se han creado las cuentas corporativas solicitadas y se ha configurado la asignación automática de permisos para el departamento de Ventas. Adjunto el listado de usuarios temporales. Quedo atento a cualquier consulta adicional. Ticket resuelto dentro del SLA."


---

## 🎫 Ticket INC-002: Usuario bloqueado y habilitación de restablecimiento de contraseña (SSPR)

* **Solicitante:** Mesa de Ayuda / Seguridad TI
* **Prioridad:** Alta (SLA: 1 hora)
* **Categoría:** Gestión de Accesos - Microsoft Entra ID

### 1. Descripción del Problema / Requerimiento
El usuario de prueba **Carlos Gómez** reporta un bloqueo de seguridad en su cuenta corporativa (`carlos.gomez@rafaeltellezitoutlook.onmicrosoft.com`) debido a múltiples intentos fallidos de inicio de sesión, requiriendo intervención del administrador para restablecer el acceso y validar el autoservicio de contraseñas (SSPR).

### 2. Procedimiento Técnico Ejecutado
1. **Simulación del Bloqueo:** Se intentó iniciar sesión con credenciales incorrectas de forma deliberada hasta activar la política de seguridad automatizada de [Microsoft Entra ID](https://github.com/copilot), generando el bloqueo temporal por motivos de seguridad.
2. **Acceso al Panel de Administración:** Se ingresó al [Portal de Azure](https://github.com/copilot) con permisos de administrador de identidades.
3. **Gestión de Credenciales y SSPR:** Se localizó al usuario en la sección **Usuarios** > **Todos los usuarios** y se ejecutó la opción de **Restablecer contraseña** para limpiar el bloqueo de seguridad, estableciendo una credencial temporal. Asimismo, se revisó el apartado de **Restablecimiento de contraseña** para configurar la directiva de autoservicio.

### 3. Verificación y Evidencias Gráficas
* **Mensaje de cuenta bloqueada en el portal de autenticación:**
 <img width="1388" height="805" alt="Captura de pantalla 2026-11-13 210634" src="https://github.com/user-attachments/assets/090c6b39-7d6e-4b68-9244-e0ec5455273f" />

* **Restablecimiento y desbloqueo exitoso en el panel de Entra ID:**
  <img width="1910" height="857" alt="Captura de pantalla 2026-11-13 211629" src="https://github.com/user-attachments/assets/7f577471-581f-4826-b9ee-50415b2b9b7c" />

* **Configuración del Autoservicio de Restablecimiento de Contraseña (SSPR):**
  <img width="1886" height="856" alt="Captura de pantalla 2026-11-13 212838" src="https://github.com/user-attachments/assets/1f62ce3b-5e3e-4e67-895c-93ea1999a978" />


### 4. Respuesta de Cierre del Ticket
"Estimado equipo: El incidente de bloqueo de cuenta para el usuario Carlos Gómez ha sido resuelto de manera exitosa. Se aplicó el restablecimiento de credenciales en Microsoft Entra ID, retirando la restricción de seguridad y validando las directivas de SSPR. Ticket cerrado dentro del SLA."


---

## 🎫 Ticket REQ-003: Exigir MFA obligatorio al área de Finanzas y políticas de acceso

* **Solicitante:** Gerencia de Seguridad de la Información / Auditoría
* **Prioridad:** Alta (SLA: 2 horas)
* **Categoría:** Acceso Condicional (Conditional Access) - Microsoft Entra ID

### 1. Descripción del Problema / Requerimiento
Se solicita implementar una directiva de seguridad proactiva para exigir **Autenticación Multifactor (MFA) obligatoria** a todos los usuarios pertenecientes al departamento de Finanzas, estructurando planes de control de identidad y evaluando restricciones geográficas en **Microsoft Entra ID**.

### 2. Procedimiento Técnico Ejecutado
1. **Definición de Arquitectura y Tecnologías:** Se diseñó la directiva considerando las capacidades de **Acceso Condicional** y **Ubicaciones con nombre** para restringir accesos y mitigar riesgos de suplantación.
2. **Evaluación de Entorno y Planes Preliminares:** Al operar en un entorno base de pruebas, se documentó la arquitectura corporativa haciendo uso de la sección de *Planes de directivas (versión preliminar)* para estructurar las reglas de cumplimiento.
3. **Estrategia de Asignación por Grupos y Controles:** Se configuró el alcance de la regla aplicando restricciones de identidad por grupos de seguridad (evitando configuraciones manuales 1x1) y estableciendo en los controles de concesión la exigencia estricta de **MFA obligatorio** para proteger las aplicaciones en la nube.

### 3. Verificación y Evidencias Gráficas
* **Creación de planes de directivas y configuración de MFA en Entra ID:**
  <img width="1920" height="1080" alt="Captura de pantalla (13)" src="https://github.com/user-attachments/assets/57faa16d-d58d-494f-8a9d-f446ee72e18f" />


### 4. Respuesta de Cierre del Ticket
"Estimado equipo: El requerimiento REQ-003 ha sido analizado, configurado y planeado exitosamente en el entorno de identidades mediante las herramientas de Acceso Condicional. Se establecieron las directivas de exigencia de MFA y segmentación por grupos para el departamento correspondiente bajo los estándares de seguridad corporativa. Ticket cerrado dentro del SLA."


---

## 🎫 Ticket INC-004: Diagnóstico de error de inicio de sesión mediante registros de auditoría

* **Solicitante:** Mesa de Ayuda / Seguridad TI
* **Prioridad:** Crítica (SLA: 30 min)
* **Categoría:** Registros de inicio de sesión y Solución de problemas - Microsoft Entra ID

### 1. Descripción del Problema / Requerimiento
Se reporta un fallo de autenticación recurrente por parte de un usuario corporativo al intentar acceder a los servicios en la nube. Se requiere realizar un diagnóstico técnico utilizando los registros de auditoría e inicio de sesión para identificar el código de error y resolver la incidencia de acceso.

### 2. Procedimiento Técnico Ejecutado
1. **Acceso a Logs de Supervisión:** Se ingresó al Portal de Azure bajo el módulo de **Microsoft Entra ID**, accediendo al apartado de *Registros de inicio de sesión* (Sign-in logs).
2. **Filtrado y Análisis de Errores:** Se revisó la traza de actividad del usuario corporativo, identificando los estados de error y los intentos de acceso para determinar la causa raíz de los fallos de autenticación.
3. **Validación de Soporte:** Se documentó el diagnóstico técnico para asegurar la resolución y la trazabilidad del incidente conforme a las métricas del SLA crítico.

### 3. Verificación y Evidencias Gráficas
* **Panel de Registros de inicio de sesión y diagnóstico en Entra ID:**
  <img width="1920" height="1080" alt="Captura de pantalla (15)" src="https://github.com/user-attachments/assets/0fd6e8a9-9b87-4cc1-bdea-98676124022e" />


### 4. Respuesta de Cierre del Ticket
"Estimado equipo: El incidente INC-004 ha sido diagnosticado exitosamente. Se analizaron los registros de inicio de sesión en Microsoft Entra ID identificando el origen del fallo de autenticación y aplicando las directrices de soporte técnico de nivel 2. Ticket cerrado dentro del SLA crítico."
