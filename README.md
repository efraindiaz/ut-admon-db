# Temario: Administración de Bases de Datos

## Unidad I: Administración de Bases de Datos Relacionales

### Tema 1: [Copias de seguridad y restauración](unidad-01/t01-backups/backup-and-restore.md)
- 🔒 Concepto de copias de seguridad.
- 🌐 Tipos de copias: Completa, Incremental, Diferencial.
- 🔎 Escenarios sugeridos para copias de seguridad.
- ⚙️ Comandos y herramientas:
  - `mysqldump` en MySQL.
  - `pg_dump` en PostgreSQL.
  - SQL Server Management Studio (SSMS).
- ✅ Protocolo de restauración.

### Tema 2: Automatización de tareas
- ⏳ Conceptos y beneficios de la automatización.
- 🔄 Tareas automatizadas comunes:
  - Respaldos automáticos.
  - Mantenimiento de índices.
  - Limpieza de datos.
- 🛠️ Herramientas para programar tareas:
  - `cron` y scripts en Linux.
  - Agente de tareas en SQL Server.

### Tema 3: Exportación e importación de datos
- 🔍 Comandos para exportar e importar datos:
  - Formatos soportados (CSV, JSON, XML).
- 🔧 Procesos de migración de datos entre sistemas.

### Tema 4: Administración de seguridad
- 🔐 Conceptos de usuarios, permisos y restricciones.
- 🔬 Configuración de acceso local y remoto.
- 🔺 Creación de esquemas de seguridad en bases de datos.

### Tema 5: Monitoreo del rendimiento
- 🔢 Identificación de herramientas de monitoreo:
  - `pgAdmin` para PostgreSQL.
  - SQL Profiler para SQL Server.
- 🔄 Análisis de rendimiento y optimización de consultas.

---

## Unidad II: Administración de Bases de Datos No Relacionales

### Tema 1: Copias de seguridad y restauración
- 🔒 Estrategias para bases no relacionales (MongoDB, Cassandra).
- ⚙️ Herramientas y protocolos para respaldos y restauraciones.

### Tema 2: Automatización de tareas
- ⏳ Configuración de tareas automatizadas:
  - Respaldos.
  - Reportes.
  - Limpieza de datos.

### Tema 3: Exportación e importación de datos
- 🔍 Formatos comunes (JSON, BSON).
- 🔧 Integración con otras herramientas y sistemas.

### Tema 4: Administración de seguridad
- 🔐 Configuración de usuarios y permisos.
- 🔬 Restricciones de acceso local y remoto.

### Tema 5: Monitoreo del rendimiento
- 🔢 Herramientas específicas (MongoDB Compass, Prometheus).
- 🔄 Análisis de uso de recursos y optimización.

---

## Unidad III: Gestión de la Calidad de Datos

### Tema 1: Definición de calidad de datos
- 🌐 Elementos clave de la calidad:
  - Exactitud.
  - Integridad.
  - Disponibilidad.
  - Confiabilidad.
  - Accesibilidad.

### Tema 2: Aseguramiento de la calidad de datos
- 🔢 Verificación y acción correctiva:
  - Actualización y normalización.
  - Eliminación de duplicados.
- 🔧 Herramientas para auditoría de calidad de datos.
