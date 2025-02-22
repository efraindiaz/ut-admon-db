
# Actividad: Automatización de Respaldo de Base de Datos MongoDB usando `mongodump` 🚀

## Objetivo 🎯

El objetivo de esta actividad es que aprendas a automatizar el proceso de respaldo de una base de datos MongoDB utilizando el comando `mongodump`. Deberás crear una base de datos de ejemplo, agregar colecciones y desarrollar un script `.bat` (para Windows) o `.sh` (para Linux/Mac) que realice el respaldo automáticamente.

## Requisitos Previos 🔧

- **Docker** instalado en tu máquina.
- **Percona Server for MongoDB** corriendo en un contenedor Docker.

## Instrucciones 📚

### Paso 1: Crear un contenedor Docker con Percona Server for MongoDB 🐳 (Omitir si ya lo tenemos listo)

[Documentación para la instalación](https://docs.percona.com/percona-server-for-mongodb/8.0/install/docker.html)
### Paso 2: Crear una base de datos y colecciones de ejemplo en MongoDB 🗃️

1. **Acceder al contenedor de MongoDB**:

   Conéctate al contenedor con el siguiente comando:

   ```bash
   docker exec -it [contenedor] bash
   ```

2. **Acceder a la shell de MongoDB**:

3. **Crear una base de datos y colecciones**:

4. **Verificar los datos**:

### Paso 3: Crear el script para realizar el respaldo automático 📑

1. **Crear el script de respaldo**:

   Debes crear un script que ejecute `mongodump` para hacer el respaldo de la base de datos. Este script puede ser un archivo `.bat` (para Windows) o `.sh` (para Linux/Mac).

2. **Hacer ejecutable el script (para Linux/Mac)**:

   Si estás usando Linux o Mac, asegúrate de que el script sea ejecutable con el siguiente comando:

   ```bash
   chmod +x mi-respaldo.sh
   ```

3. **Probar el script**:

   Ejecuta el script manualmente para verificar que funcione correctamente.

   - En **Windows**, simplemente haz doble clic en el archivo `.bat`.
   - En **Linux/Mac**, ejecuta el script desde la terminal:

     ```bash
     ./mi-respaldo.sh
     ```

   Verifica que los archivos de respaldo se hayan creado en la carpeta especificada.

### Paso 4: Automatizar el proceso ⏰

Para automatizar la ejecución del script en un horario determinado, puedes usar el **Programador de Tareas** en Windows o **cron** en Linux/Mac.

- **En Windows**: Usa el "Programador de Tareas" para crear una nueva tarea que ejecute el script `.bat` a la hora que desees.
- **En Linux/Mac**: Agrega una entrada en `crontab` para que el script se ejecute automáticamente a una hora específica. Abre el crontab con:

   ```bash
   crontab -e
   ```

   Y agrega una línea como la siguiente para ejecutar el respaldo todos los días a las 2:00 AM:

   ```bash
   0 2 * * * /ruta/a/respaldo.sh
   ```

### Paso 5: Documentar el proceso 📄

1. **Documentar los pasos**: Escribe una documentación detallada de los pasos que seguiste configurar la base de datos y las colecciones, desarrollar el script de respaldo y el proceso de automatización. 

2. **Incluir el código del script**: Asegúrate de agregar el código completo del script `.bat` o `.sh` que desarrollaste en tu documentación.

---

## Entregables 📦

- El archivo de script `.bat` o `.sh` que se creo.
- Documentación detallada de los pasos seguidos durante la actividad, incluyendo la descripción del proceso y el código del script.

---

