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
| **INC-002** | Usuario bloqueado y habilitación de restablecimiento de contraseña (SSPR) | Password Reset / Authentication Methods | Alta (1 hr) | ⏳ Pendiente |
| **REQ-003** | Exigir MFA obligatorio al área de Finanzas y bloquear accesos fuera del país | Conditional Access / Named Locations | Alta (2 hrs) | ⏳ Pendiente |
| **INC-004** | Diagnóstico de error de inicio de sesión mediante registros de auditoría | Sign-in Logs / Troubleshooting | Crítica (30 min) | ⏳ Pendiente |

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
