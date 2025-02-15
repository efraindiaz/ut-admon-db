# A01 Percona PMM

## Actividad: Instalación de Percona PMM con Docker 🚀

## Objetivo:
Instalar y configurar Percona PMM usando Docker para monitorear una base de datos MySQL. 📊

### Paso 1: Preparación del Entorno 🛠️

1. **Instalación de Docker**:
   - Si no tienes Docker instalado, instala Docker en tu máquina local o en una máquina virtual. 🖥️
   - Asegúrate de que Docker esté funcionando correctamente ejecutando `docker --version` en la terminal. ✔️

### Paso 2: Instalación de Percona PMM Server 🖧

1. **Instalación de Percona PMM Server**:
	- Investiga cómo desplegar Percona PMM Server utilizando Docker. 
	- Deberás configurar el contenedor de Percona PMM Server para que escuche en el puerto **3999**.

```bash
docker run --detach --restart always --publish 3999:8443 -v pmm-data:/srv --name pmm-server percona/pmm-server:3 
```

2. **Verificación del contenedor**: 
	- Verifica que el contenedor esté en ejecución con el siguiente comando: 

``` bash 
docker ps
``` 

- Accede a la interfaz web de Percona PMM Server en tu navegador utilizando la dirección `https://localhost:3999`. 🌐 
- Si es necesario, configura las credenciales de inicio de sesión (usuario: `admin`, contraseña: `admin` por defecto). 🔑

---
## Parte 2 - Actividad realizada en clase

### Paso 3:  Percona Server  🗂️

Paso 1: Instalacion de percona server a traves de un contenedor de Docker

Descargar y Ejecutar Percona Server con MySQL

Ejecuta el siguiente comando para descargar la imagen de Percona y ejecutar un contenedor con MySQL:

```sh
docker run -d \
  --name ps-mysql \
  -e MYSQL_ROOT_PASSWORD=root \
  -e MYSQL_DATABASE=ps_employees \
  -e MYSQL_USER=dev \
  -e MYSQL_PASSWORD=hellodev \
  -p 3998:3306 \
  --restart unless-stopped \
  percona/percona-server:latest
```

### Explicación de los parámetros:

- `--name percona-mysql` → Nombre del contenedor.
- `-e MYSQL_ROOT_PASSWORD=rootpassword` → Establece la contraseña del usuario root.
- `-e MYSQL_DATABASE=mi_base_de_datos` → Crea una base de datos por defecto.
- `-e MYSQL_USER=usuario` → Crea un usuario adicional.
- `-e MYSQL_PASSWORD=contrasena` → Asigna una contraseña al usuario adicional.
- `-p 3998:3306` → Mapea el puerto 3306 del host al contenedor.
- `--restart unless-stopped` → Asegura que el contenedor se reinicie a menos que se detenga manualmente.
- `percona/percona-server:latest` → Usa la imagen más reciente de Percona Server.

### 2. Verificar el Estado del Contenedor

Para asegurarte de que el contenedor está corriendo, ejecuta:

```sh
docker ps
```

Si necesitas ver los registros del contenedor:

```sh
docker logs percona-mysql
```

### 3. Conectarse al Servidor MySQL

Para conectarte al servidor de MySQL dentro del contenedor, usa el siguiente comando:

```sh
docker exec -it percona-mysql mysql -u root -p
```

Luego, ingresa la contraseña de root (`rootpassword` en este ejemplo).

### 4. Conexión median herramientas como Mysql Workbench

Después de habernos conectado directamente dentro del conector, es necesario verificar que nuestro puerto `9998`expone nuestro servicio fuera de nuestro contenedor.
Para esto es necesario conectarnos con alguna herramienta para verificar nuestra conexión.

## Parte 3 (Actividad)

### **Actividad: Configuración de PMM Client y Conexión con Percona Server**

### **Objetivo**

Continuar con el manual de instalación y configuración, enfocándose en la configuración de **PMM Client** para establecer la conexión entre **Percona PMM Server** y **Percona Server (MySQL)**, asegurando el monitoreo adecuado de la base de datos.

## Posibles pasos a considerar: 
- **Desplegar el cliente de Percona PMM**
- **Configurar PMM Client para conectarse a PMM Server**
- **Registrar Percona Server en PMM**
- **Verificación de la Configuración**
- **Actualización del Manual**

## Continuar el manual incluyendo:

- Descripción clara de los nuevos pasos realizados.
- Códigos utilizados y su explicación.
- Capturas de pantalla del monitoreo en PMM.
- Posibles errores y soluciones.

