# S07 Administración de seguridad

La seguridad en las bases de datos es esencial para proteger la información sensible, garantizar la integridad de los datos y prevenir accesos no autorizados.

---
### **Overview**:

- Conceptos básicos relacionados con usuarios, permisos y restricciones
- Configuración de accesos
- Creación de esquemas de seguridad.

---
## Conceptos Clave

### Usuarios, Permisos y Restricciones

- **Usuarios**: Representan a las entidades que tienen acceso a la base de datos (administradores, desarrolladores, aplicaciones, etc.).
- **Permisos**: Conceden o limitan las acciones que un usuario puede realizar (lectura, escritura, ejecución, etc.).
- **Restricciones**: Políticas o reglas que limitan cómo los usuarios pueden interactuar con la base de datos.

```sql
-- Crear un usuario
CREATE USER 'app_user'@'localhost' IDENTIFIED BY 'securepassword';

-- Asignar permisos de lectura y escritura
GRANT SELECT, INSERT, UPDATE, DELETE ON my_database.* TO 'app_user'@'localhost';

-- Aplicar los cambios
FLUSH PRIVILEGES;
```

---
### Tipos de Permisos y Restricciones

1. **Permisos por Objeto**:
    - Lectura (`SELECT`): Permite consultar los datos.
    - Escritura (`INSERT`, `UPDATE`, `DELETE`): Permite modificar o eliminar datos.
    - Ejecución (`EXECUTE`): Permite ejecutar procedimientos almacenados.
    - Alteración de estructura (`ALTER`): Permite modificar tablas, vistas, índices, etc.
2. **Permisos de Nivel Superior**:
    - Administración total (`GRANT ALL`): Concede todos los permisos.
    - Control de usuarios (`CREATE USER`, `DROP USER`): Gestiona usuarios y roles.
3. **Restricciones**:
    - Restricciones de columna: Limitar el acceso a columnas específicas en una tabla.
    - Restricciones horarias: Permitir acceso solo en horarios definidos.
    - Restricciones basadas en direcciones IP.

### Otras Configuraciones de Acceso

1. **Autenticación**:
    - Basada en contraseña.
    - Autenticación de dos factores (2FA).
    - Integración con LDAP o Active Directory para usuarios corporativos.
2. **Cifrado**:
    - Uso de conexiones cifradas (TLS/SSL)
    - Cifrado de datos en reposo y en tránsito.
3. **Limitación de conexiones simultáneas**:
    - Definir un máximo de conexiones concurrentes para usuarios específicos.


### Más Ejemplos de Restricciones

1. **Bloqueo de Regiones Geográficas**:
    - Uso de firewalls para bloquear accesos desde países no deseados.
2. **Limitaciones de Tasa (Rate Limiting)**:
    - Configurar un límite de solicitudes por minuto para evitar ataques de fuerza bruta.

---
### Configuración de Acceso Local y Remoto

- **Acceso Local**: Permite a los usuarios conectarse desde el mismo servidor donde está alojada la base de datos.
- **Acceso Remoto**: Habilita la conexión a la base de datos desde otros dispositivos.

#### Consideraciones:

1. **Habilitar conexiones remotas**:
    - Configurar el archivo de configuración de la base de datos (por ejemplo, `my.cnf` en MySQL) para permitir accesos externos.
2. **Restringir el acceso**:
    - Utilizar direcciones IP específicas para conceder permisos remotos.


Habilitar acceso remoto en MySQL:

```sql
-- Permitir acceso desde una IP específica
GRANT ALL PRIVILEGES ON my_database.* TO 'remote_user'@'192.168.1.100' IDENTIFIED BY 'securepassword';

-- Permitir acceso desde cualquier IP (no recomendado sin firewall)
GRANT ALL PRIVILEGES ON my_database.* TO 'remote_user'@'%' IDENTIFIED BY 'securepassword';

-- Aplicar los cambios
FLUSH PRIVILEGES;
```

Configuración adicional en `my.cnf`:

```
[mysqld]
bind-address = 0.0.0.0
```

---

### Creación de Esquemas de Seguridad

Un esquema de seguridad define un conjunto estructurado de permisos y restricciones que garantizan que solo las personas adecuadas puedan acceder o modificar los datos necesarios.

#### Ejemplo de Buenas Prácticas:

1. **Principio de mínimo privilegio**: Cada usuario debe tener solo los permisos necesarios para realizar sus tareas.
    
2. **Roles y grupos**:
    - Crear roles específicos para agrupar permisos comunes.
    - Asignar roles a los usuarios en lugar de permisos individuales.

#### Ejemplo  en PostgreSQL:

```sql
-- Crear un rol para lectura
CREATE ROLE reader;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO reader;

-- Crear un rol para escritura
CREATE ROLE writer;
GRANT INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA public TO writer;

-- Asignar roles a un usuario
CREATE USER 'developer' WITH PASSWORD 'securepassword';
GRANT reader, writer TO developer;
```

---

## Herramientas para la Administración de Seguridad

1. **PHPMyAdmin/MySQL Workbench**: Permite gestionar usuarios, permisos y conexiones remotas de manera gráfica.
    
2. **pgAdmin**: Herramienta para administración de bases de datos PostgreSQL, incluyendo configuraciones de seguridad.
    
3. **SQL Server Management Studio (SSMS)**: Para bases de datos SQL Server, ofrece un entorno completo para la configuración de esquemas de seguridad.
    
4. **Firewall**: Configurar reglas a nivel de servidor para restringir accesos no deseados.

