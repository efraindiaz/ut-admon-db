
# 📚 Introducción a MongoDB

Conceptos clave y aspectos avanzados de MongoDB, su estructura y funcionamiento.

## 🟢 **1. Introducción y arquitectura de MongoDB**

📝 Explica qué es **MongoDB**, su arquitectura orientada a documentos, modelo NoSQL y diferencias clave con bases de datos relacionales.

**Casos de uso y comparación con otras bases NoSQL**

- Diferencias entre MongoDB y otras bases NoSQL como **Cassandra, Redis o Firebase**.
- Cuándo es recomendable usar MongoDB frente a una base relacional o frente a otro tipo de NoSQL.
- Características Principales
- Casos de uso
## 🧩 **2. Características avanzadas**

💡 Describe características importantes: 
- **Manejo de índices**
- **Replicación**
- **Sharding**
- **Transacciones ACID**

## 📌 **3. Conceptos clave y terminología**

📖 Explica conceptos esenciales como:

- **BSON (Binary JSON)**
- **Colección y Documento:** Unidades fundamentales de almacenamiento.
- **Índices:** Mejora del rendimiento en búsquedas.
- **Aggregations:** Procesamiento avanzado de consultas.
- **Replica Sets:** Alta disponibilidad.
- **Sharding:** Escalabilidad horizontal.

## 💻 **4. Comandos y operaciones**

💾 Muestra ejemplos de comandos:

- `show dbs`
- `use`
- `db.createCollection()`
- `db.insertOne()`
- `db.find()`
- `db.updateOne()`
- `db.deleteOne()`

💾 Muestra ejemplos de comandos relevantes:

- 📊 Consultas avanzadas: `db.collection.aggregate()`
- 🔑 Manejo de índices: `db.collection.createIndex()`
- 📈 Operaciones transaccionales: `session.startTransaction()`
- 🚀 Gestión de rendimiento: `db.collection.explain()`

## 🛠️ **5. Ejemplo práctico completo**

🧪 Realiza un ejemplo que incluya:

- Creación de una base y colección.
- Inserción de documentos.
- Consultas con filtros y agregaciones.
- Indexación.

## 💡 **6. Conclusión y reflexiones**

🗨️ Reflexiona sobre las ventajas y casos de uso de MongoDB frente a otras bases de datos, considerando escenarios de alta demanda y escalabilidad.
