# 📘 Configuración Final: Conexión de Percona Server for MongoDB con PMM

## 🎯 **Objetivo**

Finalizar el manual de instalación y configuración del entorno de monitoreo con Percona PMM, integrando **Percona Server for MongoDB** al dashboard de monitoreo. Se debe continuar con la actividad previa y documentar el proceso final de configuración.

---

## 🛠 **Pasos a Seguir**

### 1️⃣ **Desplegar Percona Server for MongoDB en Docker**

- Utilizar una imagen de **Percona Server for MongoDB**.
- Configurar los volúmenes y puertos necesarios.
- Verificar que la base de datos esté corriendo correctamente.

### 2️⃣ **Instalar y Configurar PMM Client para MongoDB**

- Se puede utilizar el mismo nodo ya creado para **Percona Server for MySQL** y simplemente registrar un nuevo servicio para MongoDB.
- Asegurarse de que el **PMM Client** esté instalado en la máquina donde corre MongoDB.
- Conectar el PMM Client con el PMM Server ya configurado.
- Para más detalles, seguir la documentación oficial: [Percona PMM - MongoDB Integration](https://docs.percona.com/percona-monitoring-and-management/3/install-pmm/install-pmm-client/connect-database/mongodb.html).

### 3️⃣ **Registrar Percona Server for MongoDB en PMM**

- Existen dos opciones para agregar el servicio de monitoreo de MongoDB:
    - 📌 **Vía línea de comandos**, utilizando `pmm-admin` para registrar el nuevo servicio.
    - 🖥 **Directamente desde el Dashboard de Percona PMM**, agregando el servicio en la interfaz gráfica.
- Configurar las opciones necesarias para el monitoreo adecuado de la base de datos.
- Consultar la guía oficial para asegurar la correcta configuración: [Percona PMM - MongoDB Integration](https://docs.percona.com/percona-monitoring-and-management/3/install-pmm/install-pmm-client/connect-database/mongodb.html).

### 4️⃣ **Verificación de la Configuración**

- Acceder al **Dashboard de PMM**.
- Validar que los métricos de **MongoDB** aparezcan correctamente en la interfaz.

### 5️⃣ **Actualizar el Manual de Instalación**

Se debe complementar la documentación con:

- 📌 **Descripción clara** de los nuevos pasos realizados.
- 📝 **Códigos utilizados** y su explicación.
- 📸 **Capturas de pantalla** del monitoreo en PMM.
- ❌ **Posibles errores y soluciones** encontradas durante la configuración.

### 6️⃣ **Conclusión**

Al final del documento, incluir una breve reflexión sobre el entorno de monitoreo configurado, algunos puntos que podemos considerar:

- 📊 La importancia de contar con un monitoreo centralizado.
- 🚀 Beneficios obtenidos con la integración de **Percona PMM**.
- 🔍 Retos encontrados durante la configuración y cómo fueron superados.

---

## 📄 **Entrega**

- 📚 Documentación bien estructurada, clara y detallada.
- 📂 Entrega en formato **PDF**.
- 📌 Se evaluará la calidad del contenido, organización y claridad en las explicaciones.
