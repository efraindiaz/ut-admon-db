# Terminal

## 1. Conexión a MySQL desde la Consola

Para conectarte a MySQL:

### 1.1. Abrir la consola de MySQL

- **Windows**: Abre "MySQL Command Line Client" desde el menú Inicio.
- **Mac/Linux**: Abre una terminal y ejecuta:
    
    ```bash
    mysql -u root -p
    ```
    
    Donde `root` es el nombre de usuario y se te pedirá la contraseña configurada durante la instalación.

### 1.2. Comandos básicos de conexión

- Para conectarte a un servidor remoto:
    
    ```bash
    mysql -u [user] -p -h [host] -P [port]
    ```
    
    Example:
    
    ```bash
    mysql -u admin -p -h 192.168.1.100 -P 3306
    ```
    
- Para salir de la consola:
    
    ```bash
    exit
    ```
    

---

## 2. Comandos Básicos en MySQL

### 2.1. Mostrar bases de datos

Para listar todas las bases de datos disponibles:

```sql
SHOW DATABASES;
```

### 2.2. Seleccionar una base de datos

Para usar una base de datos específica:

```sql
USE database_name;
```

### 2.3. Crear una base de datos

Para crear una nueva base de datos:

```sql
CREATE DATABASE database_name;
```

### 2.4. Eliminar una base de datos

Para eliminar una base de datos:

```sql
DROP DATABASE database_name;
```

---

## 3. Operaciones con Tablas

### 3.1. Crear una tabla

```sql
CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(50) NOT NULL,
  email VARCHAR(50) UNIQUE,
  age INT
);
```

### 3.2. Insertar datos en una tabla

```sql
INSERT INTO users (name, email, age) 
VALUES ('John Doe', 'john@example.com', 30);
```

### 3.3. Consultar datos

- Obtener todos los datos:
    
    ```sql
    SELECT * FROM users;
    ```
    
- Obtener datos específicos:
    
    ```sql
    SELECT name, email FROM users WHERE age > 25;
    ```
    

### 3.4. Actualizar datos

```sql
UPDATE users 
SET age = 31 
WHERE name = 'John Doe';
```

### 3.5. Eliminar datos

```sql
DELETE FROM users 
WHERE email = 'john@example.com';
```

---
