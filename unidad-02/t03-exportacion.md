# 🚀 **Tema 3: Exportación e Importación de Datos en MongoDB**

## 🔄 **1. ETL: Extract, Transform, Load (Extracción, Transformación y Carga)**

El proceso **ETL** es fundamental para mover y transformar datos entre sistemas. Se divide en tres fases:

1. **🛠 Extract (Extracción):** Se obtienen datos desde diferentes fuentes, como bases de datos, archivos o APIs. En MongoDB, se pueden extraer datos con `mongoexport` o desde código con `mongodb` en Node.js.
2. **🔄 Transform (Transformación):** Se limpian, convierten y estructuran los datos según las necesidades del sistema destino.
3. **📥 Load (Carga):** Se insertan los datos en el sistema de destino, como otro servidor MongoDB o una base de datos SQL.

### ✨ **Ejemplo de ETL en MongoDB con Node.js:**
```javascript
const { MongoClient } = require("mongodb");
const fs = require("fs");

const url = "mongodb://localhost:27017";
const dbName = "empresa";
const client = new MongoClient(url);

async function etlProcess() {
    try {
        await client.connect();
        const db = client.db(dbName);
        const collection = db.collection("empleados");
        
        // 📤 Extracción: Obtener datos desde MongoDB
        const empleados = await collection.find({}).toArray();
        
        // 🔍 Transformación: Filtrar empleados mayores de 25 años
        const empleadosFiltrados = empleados.filter(emp => emp.edad > 25);
        
        // 💾 Carga: Guardar en un archivo JSON
        fs.writeFileSync("empleados_filtrados.json", JSON.stringify(empleadosFiltrados, null, 2));
        
        console.log("Proceso ETL completado");
    } catch (err) {
        console.error(err);
    } finally {
        await client.close();
    }
}

etlProcess();
```

---

## 📂 **2. Formatos Comunes de Exportación e Importación**

### **📜 JSON (JavaScript Object Notation)**

✔ Formato ligero y fácil de leer.
✔ Compatible con la mayoría de los lenguajes de programación.
✔ Se usa ampliamente para importar y exportar datos en MongoDB.

Ejemplo de un documento JSON:

```json
{
  "nombre": "Juan Pérez",
  "edad": 30,
  "correo": "juan@example.com",
  "activo": true
}
```

### **⚡ BSON (Binary JSON)**

✔ Formato binario utilizado internamente por MongoDB.
✔ Soporta tipos de datos adicionales como fechas y binarios.
✔ Más eficiente en almacenamiento y velocidad.

---

## 📤 **3. Exportación de Datos en MongoDB**
MongoDB ofrece `mongoexport` para exportar datos en **JSON** o **CSV**.

### **Ejemplo 1: Exportar a JSON**
```bash
mongoexport --db miBaseDeDatos --collection usuarios --out usuarios.json
```

### **Ejemplo 2: Exportar a CSV**
```bash
mongoexport --db miBaseDeDatos --collection usuarios --type=csv --fields nombre,edad,correo --out usuarios.csv
```

---

## 📥 **4. Importación de Datos en MongoDB**
MongoDB proporciona `mongoimport` para importar datos en **JSON** o **CSV**.

### **Ejemplo 1: Importar desde JSON**

```bash
mongoimport --db miBaseDeDatos --collection usuarios --file usuarios.json --jsonArray
```

### **Ejemplo 2: Importar desde CSV**

```bash
mongoimport --db miBaseDeDatos --collection usuarios --type=csv --headerline --file usuarios.csv
```

---

## 🔗 **5. Integración con Otras Herramientas y Sistemas**

### **🖥 Conectando MongoDB con Node.js**
Se puede usar la librería `mongodb` para manejar exportaciones e importaciones.

Ejemplo:
```javascript
const { MongoClient } = require("mongodb");
const fs = require("fs");

const url = "mongodb://localhost:27017";
const dbName = "ps_employees_mongo";
const client = new MongoClient(url);

async function exportToJSON() {
    try {
        await client.connect();
        const db = client.db(dbName);
        const collection = db.collection("employees");
        
        // 📤 Extracción: Obtener datos desde MongoDB
        const employees = await collection.find({}, { projection: { _id: 0 } }).toArray();
        
        // 💾 Guardar en un archivo JSON
        fs.writeFileSync("employees.json", JSON.stringify(employees, null, 2));
        console.log("Exportación completada");
    } catch (err) {
        console.error(err);
    } finally {
        await client.close();
    }
}

exportToJSON();
```

### **🛠 Herramientas ETL Populares para MongoDB**
✔ **Apache NiFi** – Para automatizar flujos de datos.
✔ **Pentaho Data Integration** – Para transformar y cargar datos en MongoDB.
✔ **Talend** – Para extracción y transformación de datos en diferentes formatos.

---

## 🎯 **6. Puntos importantes**

✅ JSON y BSON son los principales formatos de datos en MongoDB.
✅ `mongoexport` y `mongoimport` facilitan la transferencia de datos.
✅ El proceso **ETL** ayuda a gestionar la migración y transformación de datos.
✅ MongoDB se integra con herramientas de desarrollo y análisis de datos.

---

