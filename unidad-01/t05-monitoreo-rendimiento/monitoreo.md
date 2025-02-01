# S08 Monitoreo

## **Monitoreo del Rendimiento en Bases de Datos**

### **Objetivo General:**

Comprender la importancia del monitoreo del rendimiento en bases de datos, identificar herramientas disponibles y analizar cómo optimizar consultas para mejorar el desempeño.

---

### **1. Identificación de herramientas de monitoreo** 🔢

Las herramientas de monitoreo permiten identificar cuellos de botella, optimizar el uso de recursos y asegurar que la base de datos funcione eficientemente. Existen varias herramientas que ayudan a los administradores a supervisar la salud y el rendimiento del sistema.

#### **Herramientas comunes:**

1. **PHPMyAdmin/MySQL Workbench**:
    - Ofrece herramientas visuales para monitoreo de consultas.
    - Permite visualizar el estado de los índices, conexiones activas y uso de CPU.
2. **pgAdmin (PostgreSQL)**:
    - Herramienta gráfica que permite supervisar la actividad de sesiones y rendimiento general.
    - Incluye estadísticas de consultas y análisis de índices.
3. **SQL Server Management Studio (SSMS)**:
    - Ofrece reportes de actividad de la base de datos, planes de ejecución y análisis de uso de índices.
4. **Herramientas de terceros**:
    - **New Relic**: Monitoreo de aplicaciones y bases de datos en tiempo real.
    - **Datadog/AppDynamics**: Supervisión integral de rendimiento, consumo de recursos y consultas.
    - **SolarWinds Database Performance Analyzer**: Identifica problemas y optimiza el rendimiento de múltiples motores de base de datos.
5. **Monitoreo con sistemas open-source**:
    - **Prometheus + Grafana**: Sistema de monitoreo de métricas y visualización en tiempo real.
    - **Zabbix**: Permite monitorear servidores y bases de datos con alertas configurables.

#### **Monitoreo con MySQL Workbench**

```sql
SHOW FULL PROCESSLIST;
-- Muestra las conexiones activas en la base de datos y el estado de las consultas en ejecución.

SHOW STATUS LIKE 'Threads_running';
-- Indica la cantidad de hilos que están ejecutándose activamente.

```

---

### **2. Análisis de rendimiento y optimización de consultas** 🔄

#### **Importancia del análisis de consultas:**

Las consultas ineficientes son una de las principales causas de bajo rendimiento en una base de datos. Optimizar las consultas mejora los tiempos de respuesta y reduce la carga del servidor.

#### **Pasos para optimizar consultas:**

1. **Analizar el plan de ejecución**: Emplear comandos o herramientas gráficas para observar cómo se ejecuta una consulta y detectar posibles mejoras.
    - En **MySQL**:
```sql
    EXPLAIN SELECT * FROM employees WHERE position = 'SALES';
```
	
    - En **PostgreSQL**:
```sql
    EXPLAIN ANALYZE SELECT * FROM employees WHERE department = 'SALES';
```

        
2. **Revisar índices**:
    
    - Los índices permiten que las consultas sean más rápidas al reducir la cantidad de datos que se deben buscar.
        
3. **Reducir columnas seleccionadas**:
    
    - En lugar de usar `SELECT *`, especifica únicamente las columnas necesarias.
    -
    ```sql
	 SELECT name, salary FROM employees WHERE department = 'Sales';
    ```
        
4. **Paginar resultados**:
    
    - Si esperas muchos registros, utiliza la paginación para limitar la cantidad de datos devueltos.
        
    ```sql
    SELECT * FROM employees LIMIT 10 OFFSET 20;
    ```
        
5. **Optimizar subconsultas**:
    - Transforma subconsultas en uniones (joins) cuando sea posible.
    - Ejemplo:
```sql
-- Subconsulta ineficiente 
SELECT name FROM employees WHERE department_id = (SELECT id FROM departments WHERE name = 'Sales');  
-- Mejora con JOIN 
SELECT e.name  FROM employees e JOIN departments d ON e.department_id = d.id WHERE d.name = 'Sales';
```
        
6. **Monitorizar métricas de consultas**:
    
    - Usa herramientas como el **Query Profiler** en MySQL o el **Query Store** en SQL Server.


### Optimización de una consulta en MySQL.

```sql
-- Consulta inicial 
SELECT *  FROM orders  WHERE customer_id = 123 AND order_date >= '2025-01-01';  -- Optimización: Añadir un índice 
CREATE INDEX idx_customer_order ON orders(customer_id, order_date);
```

#### **Actividades comunes de análisis y optimización:**

- Identificar consultas que consumen más recursos.
- Reducir los escaneos completos de tablas.
- Eliminar redundancias en consultas.
