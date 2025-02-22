
# 🌿 MongoDB: Base de Datos NoSQL Versátil y Potente

MongoDB es una base de datos NoSQL muy popular y flexible, ideal para almacenar y gestionar datos complejos.

---

## 1️⃣ Modelo de Datos Orientado a Documentos 📄  

- Almacena datos en documentos BSON (Binary JSON), una representación binaria de JSON.  
- Los documentos pueden tener estructuras flexibles, lo que permite almacenar datos con distintos campos y tipos.  
- Esta flexibilidad facilita el desarrollo de aplicaciones que manejan datos complejos y en constante evolución.  

---

## 2️⃣ Base de Datos NoSQL 🚀  

- MongoDB no utiliza el lenguaje SQL tradicional; en su lugar, emplea un lenguaje de consulta basado en documentos y operadores.  
- Las bases de datos NoSQL son ideales para aplicaciones que requieren alta escalabilidad y flexibilidad.  

---

## 3️⃣ Escalabilidad Horizontal ⚙️  

- MongoDB está diseñada para escalar horizontalmente mediante *sharding*.  
- Distribuye los datos en múltiples servidores para manejar grandes volúmenes de información y tráfico.  
- Esta capacidad la convierte en una excelente opción para aplicaciones con muchos usuarios y peticiones simultáneas.  
### ¿Cómo funciona?

1. **Sharding**: Los datos se dividen en fragmentos más pequeños (shards) y se distribuyen en diferentes servidores. Cada shard contiene una parte de los datos.
2. **Servidor de enrutamiento**: Un servidor de enrutamiento dirige las consultas a los shards correspondientes.
3. **Servidores de configuración**: Los servidores de configuración almacenan metadatos sobre la distribución de los datos en los shards.

### Beneficios

- **Mayor rendimiento**: Al distribuir la carga de trabajo, se reduce el tiempo de respuesta y se mejora el rendimiento general.
- **Mayor capacidad**: Se pueden agregar más shards para aumentar la capacidad de almacenamiento y procesamiento.
- **Mayor disponibilidad**: Si un shard falla, los demás shards pueden seguir funcionando.

---

## 4️⃣ Replicación y Alta Disponibilidad 🔄  

- MongoDB ofrece replicación mediante *replica sets* para garantizar la alta disponibilidad.  
- Si un servidor falla, otro servidor replica toma el control automáticamente, asegurando la continuidad del servicio.  
### ¿Cómo funciona?

1. **Conjunto de réplicas**: Un conjunto de réplicas es un grupo de servidores que contienen copias de los mismos datos.
2. **Nodo primario**: Uno de los servidores es el nodo primario, que recibe todas las escrituras.
3. **Nodos secundarios**: Los demás servidores son nodos secundarios, que replican los datos del nodo primario.
4. **Conmutación por error automática**: Si el nodo primario falla, uno de los nodos secundarios se convierte automáticamente en el nuevo nodo primario.

### Beneficios

- **Alta disponibilidad**: Los datos están disponibles incluso si uno o varios servidores fallan.
- **Tolerancia a fallos**: El sistema puede seguir funcionando sin interrupciones si un nodo falla.
- **Lecturas escalables**: Las lecturas se pueden distribuir en los nodos secundarios para mejorar el rendimiento.

---

## 5️⃣ Características Principales 🛠️  

- 🏷️ **Índices:** Permiten mejorar el rendimiento de las consultas.  
- 📊 **Framework de Agregación:** Facilita análisis complejos de los datos.  
- 🔍 **Consultas Avanzadas:** Soporta búsquedas simples, geoespaciales y de texto.  
- 🔒 **Transacciones ACID:** Garantizan la integridad de los datos en operaciones críticas.  

---

## 6️⃣ Casos de Uso 🌐  
- Aplicaciones web y móviles.  
- Sistemas de análisis de datos.  
- Aplicaciones de IoT (Internet de las Cosas).  
- Plataformas que requieren escalabilidad y rendimiento constante.  

---

## 7️⃣ Comunidad y Recursos 🤝  
- MongoDB cuenta con una gran comunidad global que ofrece soporte, herramientas y buenas prácticas.  
- 📖 **MongoDB University:** Cursos gratuitos y de pago para aprender desde los conceptos básicos hasta técnicas avanzadas.  

---

🎯 **Conclusión:**  
MongoDB es una excelente opción para proyectos que necesitan una base de datos flexible, escalable y de alto rendimiento. Su modelo orientado a documentos y su potente ecosistema la convierten en una herramienta imprescindible en el desarrollo moderno.  

---


## 📥 1. Instalación

### 🖥️ Instalación de MongoDB Community Edition

#### Windows

4. Descarga el instalador desde el [Centro de Descargas de MongoDB](https://www.mongodb.com/try/download/community).
5. Ejecuta el instalador con la configuración predeterminada y asegúrate de seleccionar "Install MongoDB Compass".
6. Agrega MongoDB a la variable PATH del sistema.

#### macOS

```bash
brew tap mongodb/brew
brew install mongodb-community
```

_Este comando utiliza Homebrew, un gestor de paquetes para macOS, para instalar la edición comunitaria de MongoDB._

#### Linux (Ubuntu)

```bash
sudo apt update
sudo apt install -y mongodb
```

_Esto actualizará el índice de paquetes e instalará MongoDB._

### 🚀 Iniciar el Servicio de MongoDB

```bash
# Windows
net start MongoDB

# macOS y Linux
brew services start mongodb-community
sudo systemctl start mongodb
```

_Estos comandos inician el servicio de MongoDB en el sistema._

### 🧪 Verificar Instalación

```bash
mongo --version
```

_Este comando verifica si MongoDB se instaló correctamente._

---

## ⚙️ 2. Conectar a MongoDB

### Conexión Local

```bash
mongo
```

_Este comando abre una sesión de la shell de MongoDB para conectarse a una base de datos local._

### Conexión Remota

```bash
mongo "mongodb+srv://<username>:<password>@cluster0.mongodb.net/test"
```

_Aquí se establece una conexión remota a una base de datos MongoDB alojada en la nube._

### Conexión con Node.js

```javascript
const { MongoClient } = require('mongodb');

const uri = "mongodb://localhost:27017";
const client = new MongoClient(uri);

async function connectDB() {
  try {
    await client.connect();
    console.log("Connected to MongoDB!");
  } catch (err) {
    console.error("Connection failed", err);
  } finally {
    await client.close();
  }
}

connectDB();
```

_Este fragmento de código muestra cómo conectarse a MongoDB utilizando Node.js._

---

## 🗂️ 3. Operaciones con Bases de Datos

### Crear una Base de Datos

```javascript
use myDatabase
```

_Este comando crea una nueva base de datos llamada "myDatabase" o cambia a ella si ya existe._

### Mostrar Bases de Datos

```javascript
show dbs
```

_Muestra una lista de todas las bases de datos disponibles en el servidor._

### Eliminar una Base de Datos

```
db.dropDatabase()
```

_Este comando elimina la base de datos activa._

---

## 📄 4. Operaciones con Colecciones

### Crear una Colección

```
db.createCollection("users")
```

_Este comando crea una colección llamada "users"._

### Mostrar Colecciones

```
show collections
```

_Muestra todas las colecciones dentro de la base de datos activa._

### Eliminar una Colección

```
db.users.drop()
```

_Este comando elimina la colección "users"._

---

## 🛠️ 5. Operaciones CRUD

### 🟢 Crear (Create)

```javascript
db.users.insertOne({ name: "John", age: 30, email: "john@example.com" })

db.users.insertMany([
  { name: "Jane", age: 25 },
  { name: "Mike", age: 35 }
])
```

_Estos comandos insertan uno o múltiples documentos en la colección "users"._

### 🔍 Leer (Read)

```javascript
db.users.find()
db.users.find({ age: { $gt: 25 } })
db.users.findOne({ name: "John" })
```

_Estos comandos permiten leer documentos de una colección con diferentes criterios de búsqueda._

### 🛠️ Actualizar (Update)

```javascript
db.users.updateOne({ name: "John" }, { $set: { age: 31 } })
db.users.updateMany({}, { $set: { active: true } })
```

_Actualizan uno o más documentos en función de una condición dada._

### 🗑️ Eliminar (Delete)

```javascript
db.users.deleteOne({ name: "John" })
db.users.deleteMany({ age: { $lt: 25 } })
```

_Estos comandos eliminan documentos basándose en criterios específicos._

---

## 🧠 6. Índices (Indexing)

### Crear un Índice

```javascript
db.users.createIndex({ email: 1 })
```

_Este comando crea un índice ascendente en el campo "email" para mejorar la velocidad de las consultas._

### Listar Índices

```javascript
db.users.getIndexes()
```

_Muestra todos los índices creados en la colección._

---

## 🔒 7. Conceptos Básicos de Seguridad

### Crear un Usuario

```javascript
db.createUser({
  user: "admin",
  pwd: "securePassword",
  roles: [ { role: "readWrite", db: "myDatabase" } ]
})
```

_Este comando crea un usuario con permisos de lectura y escritura en "myDatabase"._

### Autenticar un Usuario

```javascript
db.auth("admin", "securePassword")
```

_Autentica al usuario especificado en la base de datos._

---

## 🌐 8. Copia de Seguridad y Restauración

### Realizar una Copia de Seguridad

```bash
mongodump --db=myDatabase --out=/backup
```

_Este comando genera una copia de seguridad de la base de datos "myDatabase" en la carpeta "/backup"._

### Restaurar una Copia de Seguridad

```bash
mongorestore --db=myDatabase /backup/myDatabase
```

_Este comando restaura la base de datos desde una copia previamente creada._

---

[Video practica MongoDB Grupo-IDYGS82:](https://www.canva.xcom/design/DAGfwh5DHIM/Hu2Q8-gtcz48GALnJAK3tw/edit?utm_content=DAGfwh5DHIM&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton)
