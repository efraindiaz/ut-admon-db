# 🏢 Plan de Administración de Bases de Datos No Relacionales con MongoDB 📊

## 1. 💡 Introducción y Caso de Estudio

### 1.1 🎯 Objetivo y Alcance del Documento
Se deberá realizar la adecuación del Plan de Administración de Bases de Datos previamente elaborado, adaptándolo a MongoDB 🛠️ como base de datos no relacional. El objetivo es definir estrategias de administración para garantizar el correcto funcionamiento, seguridad y respaldo de la base de datos en un entorno NoSQL.

### 1.2 📅 Contexto del Caso de Estudio y Escenario Específico
Plantear un caso de estudio donde se requiera el uso de MongoDB y describir su importancia en el almacenamiento y gestión de los datos. Además, incluir una descripción detallada del contexto y los requisitos operativos de la base de datos, estableciendo:

- 🏨 **Cadena Hotelera**: Gestión de reservas y clientes.
- 🛒 **E-commerce**: Manejo de catálogo de productos y transacciones.
- 🏥 **Clínica/Hospital**: Registro de historias clínicas y citas médicas.

**Aspectos clave:**
- 💡 **Función principal del sistema**: Definir el propósito de la base de datos (por ejemplo, almacenar pedidos, gestionar inventarios, etc.).
- 🚨 **Nivel de criticidad de los datos**: Analizar la importancia de la información almacenada y el impacto de una interrupción o pérdida de datos.

## 2. 🛠️ Procedimiento de Copias de Seguridad

- 💾 Tipos de respaldo en MongoDB (backup completo, incremental y snapshots).
- 🛠️ Herramientas utilizadas: `mongodump`, `mongorestore`, MongoDB Atlas Backups.
- 🕒 Cronograma de ejecución: Frecuencia y horarios de respaldos.

## 3. 🔄 Protocolos de Restauración

- 📐 Procedimiento detallado para recuperar datos desde un respaldo.
- 🔧 Uso de `mongorestore` y consideraciones al restaurar bases de datos de gran tamaño.

## 4. 🤖 Automatización de Tareas

- 🔽 Automatización de copias de seguridad con `cron` en Linux o `Task Scheduler` en Windows.
- 🎨 Implementación de scripts de mantenimiento con Node.js o Python.

## 5. 📚 Métodos de Importación y Exportación de Datos

- 📝 Uso de `mongoimport` y `mongoexport` con ejemplos de comandos.
- 🌐 Integración con herramientas ETL si aplica.

## 6. 🔒 Lineamientos de Seguridad

- 🔐 Control de acceso y roles de usuario en MongoDB.
- ⚖️ Configuración de autenticación y autorización.
- 🔎 Auditoría y protección de datos sensibles.
- 🔑 Cifrado en reposo y en tránsito.

## 7. 🔄 Formato del Documento

- **🌟 Fuente**: Arial o Times New Roman.
- **📅 Tamaños**: Título 16pt, Subtítulo 14pt, Contenido 12pt.
- **📜 Interlineado**: 1.5.
- **🔷 Márgenes**: 2.5 cm en todos los lados.
- **📑 Numeración**: Secciones numeradas y organizadas.
- **📄 Formato final**: PDF.

