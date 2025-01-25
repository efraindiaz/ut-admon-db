#Herramientas para automatización

### **1. Herramientas nativas de los DBMS**

#### **MySQL**

- **Eventos (Event Scheduler)**: Permite programar tareas directamente en el servidor.
```sql
CREATE EVENT my_event ON SCHEDULE EVERY 1 DAY DO DELETE FROM logs WHERE created_at < NOW() - INTERVAL 30 DAY;
```
    
- **Herramienta de línea de comandos (`mysqldump`)**: Para respaldos automáticos.
- **Triggers**: Ejecutan acciones en respuesta a eventos DML (INSERT, UPDATE, DELETE).

#### **PostgreSQL**

- **pgAgent**: Extensión para programar tareas en PostgreSQL.
- **Herramienta de línea de comandos (`pg_dump`)**: Para respaldos automáticos.
- **Triggers y reglas**: Permiten manejar tareas como auditoría o transformaciones automáticas.

#### **SQL Server**

- **SQL Server Agent**: Administra y programa tareas en SQL Server.
- **Mantenimiento de bases de datos**: Programación de índices, estadísticas y backups.

#### **Oracle**

- **DBMS_SCHEDULER**: API de programación avanzada de Oracle.
- **Triggers y procedimientos almacenados**.

---

### **2. Cron Jobs y Programadores de Tareas**

Puedes utilizar herramientas del sistema operativo para ejecutar scripts relacionados con bases de datos.

#### **En Linux**

- **Cron**: Agenda comandos o scripts, como respaldos o limpieza de datos.
```bash
0 2 * * * /usr/bin/mysqldump -u root -p password database > /backups/backup.sql
```    

#### **En Windows**

- **Programador de Tareas**: Configura tareas para ejecutar scripts o comandos.
    - Ejemplo: Ejecutar un script `.bat` que ejecute `pg_dump`.

---

### **3. Herramientas de orquestación y automatización**

- **Airflow**: Framework para orquestación de flujos de trabajo, compatible con bases de datos.
- **Apache NiFi**: Permite procesar, transformar y programar flujos de datos.
- **Luigi**: Similar a Airflow, para pipelines de datos.
