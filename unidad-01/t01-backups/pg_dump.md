# S04 PG_DUMP

- Conectarse a PostgreSQL
- Crear una base de datos
- Definir una tabla
- Insertar datos
- Realizar un respaldo utilizando `pg_dump`

## Prerrequisitos

- PostgreSQL instalado en tu sistema.
- Acceso a la terminal o línea de comandos.
- Usuario con permisos suficientes para interactuar con PostgreSQL.

export PATH=$PATH:/Library/PostgreSQL/17/bin

---

## 1. Conectarse a PostgreSQL

Para conectarte a PostgreSQL desde la terminal:

```bash
psql -U <usuario> -h <host> -d <nombre_base_datos>
```

**Significado de los parámetros:**

- `-U`: Especifica el nombre del usuario de PostgreSQL.
- `-h`: Define el host donde se encuentra el servidor de PostgreSQL (por ejemplo, `localhost`).
- `-d`: Indica el nombre de la base de datos a la que deseas conectarte.

**Ejemplo:** Si tu usuario es `postgres` y deseas conectarte a la base de datos `postgres` (base predeterminada):

```bash
psql -U postgres -h localhost -d postgres
```

Te pedirá la contraseña del usuario `postgres`.

---

## 2. Crear una Base de Datos

Dentro de PostgreSQL, ejecuta el siguiente comando para crear una base de datos llamada `school`:

```sql
CREATE DATABASE school;
```

Sal de la sesión actual y conecta nuevamente, esta vez a la base de datos `school`:

```bash
psql -U postgres -h localhost -d school
```

---

## 3. Crear una Tabla

Una vez conectado a la base de datos `school`, crea una tabla llamada `students`:

```sql
CREATE TABLE students (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    age INT NOT NULL,
    grade VARCHAR(10)
);
```

---

## 4. Insertar Datos en la Tabla

Inserta algunos datos en la tabla `students`:

```sql
INSERT INTO students (name, age, grade) VALUES
('Alice', 14, '8th'),
('Bob', 15, '9th'),
('Charlie', 13, '7th');
```

Verifica que los datos fueron agregados correctamente:

```sql
SELECT * FROM students;
```

---

## 5. Realizar un Respaldo con `pg_dump`

El comando `pg_dump` se utiliza para crear respaldos de bases de datos en PostgreSQL.

### 5.1 Respaldo Completo

Para generar un respaldo completo de la base de datos `school` en formato SQL:

```bash
pg_dump -U postgres -h localhost -d school -f school_backup.sql
```

**Significado de los parámetros:**

- `-U`: Especifica el usuario de PostgreSQL.
- `-h`: Define el host del servidor de PostgreSQL.
- `-d`: Indica el nombre de la base de datos a respaldar.
- `-f`: Especifica el archivo donde se guardará el respaldo.

Este comando crea un archivo llamado `school_backup.sql` que contiene todos los comandos SQL necesarios para recrear la base de datos.

### 5.2 Respaldo de una Tabla Específica

Si solo deseas respaldar la tabla `students`:

```bash
pg_dump -U postgres -h localhost -d school -t students -f students_backup.sql
```

**Significado adicional:**

- `-t`: Indica que solo se debe respaldar la tabla especificada (en este caso, `students`).

### 5.3 Respaldo en Formato Personalizado

Puedes usar el formato personalizado de PostgreSQL para respaldos:

```bash
pg_dump -U postgres -h localhost -d school -Fc -f school_backup_custom.dump
```

**Significado adicional:**

- `-Fc`: Especifica que el respaldo debe estar en formato personalizado.

Este archivo puede ser restaurado usando `pg_restore`.

---

## 6. Restaurar un Respaldo

### 6.1 Restaurar desde un Respaldo SQL

Para restaurar un respaldo en formato SQL, conéctate a PostgreSQL y usa el comando `psql`:

```bash
psql -U postgres -h localhost -d school < school_backup.sql
```

### 6.2 Restaurar desde un Respaldo Personalizado

Si usaste el formato personalizado:

```bash
pg_restore -U postgres -h localhost -d school school_backup_custom.dump
```

---

## Conclusión

Este manual te proporciona los pasos básicos para interactuar con PostgreSQL y realizar respaldos con `pg_dump`. Ahora puedes proteger tus datos y gestionar tus bases de manera eficiente.


