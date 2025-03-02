# Instalación de Percona

- Percona PMM Server
- Percona Server
- Percona Client
- Percona Server for MongoDB

---
## Percona PMM Server

**Image**

```shell
docker pull percona/pmm-server:3
```

**Volume**

```shell
docker volume create pmm-data
```

**Contenedor**

```shell
docker run --detach --restart always --publish 3999:8443 -v pmm-data:/srv --name pmm-server percona/pmm-server:3
```

Comando completo

```shell
docker pull percona/pmm-server:3 && \
docker volume create pmm-data && \
docker run --detach --restart always --publish 3999:8443 -v pmm-data:/srv --name pmm-server percona/pmm-server:3
```

---
## Percona Server For MySQL

**Contenedor**

```shell
docker run -d \
  --name ps-mysql \
  -e MYSQL_ROOT_PASSWORD=root \
  -e MYSQL_DATABASE=ps_employees \
  -e MYSQL_USER=dev \
  -e MYSQL_PASSWORD=devpass \
  -p 3998:3306 \
  --restart unless-stopped \
  percona/percona-server:latest
  ```

**Validación**

```bash
docker exec -it ps-mysql bash
```

**Conexión BD**

```sh
mysql -u root -p
```
---
## PMM Client

### # Run PMM Client as a Docker container
Información de la documentación de Percona 

Pull the PMM Client Docker image:

```shell
  docker pull percona/pmm-client:3
```

Create a Docker volume to store persistent data:

```shell
docker volume create pmm-client-data
```

Percona PMM Server Container IP

```shell
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' pmm-server
```

```shell
docker run -d \
  --name pmm-client \
  -e PMM_AGENT_SERVER_ADDRESS=172.17.0.2:8443 \
  -e PMM_AGENT_SERVER_USERNAME=admin \
  -e PMM_AGENT_SERVER_PASSWORD=admin \
  -e PMM_AGENT_SERVER_INSECURE_TLS=1 \
  -e PMM_AGENT_CONFIG_FILE=config/pmm-agent.yaml \
  -v pmm-client-data:/srv \
  percona/pmm-client:3
```

Registra el nodo del cliente con PMM Server

```shell
docker exec pmm-client pmm-admin config \
--server-insecure-tls \
--server-url=http://admin:admin@172.17.0.2:8443 \
172.17.0.4 container ps-dk-container \
--force
```

### Explicación

1. **`docker exec pmm-client`**  
    Ejecuta un comando dentro del contenedor `pmm-client`. En este caso, se ejecuta `pmm-admin config`.
    
2. **`pmm-admin config`**  
    Es el comando de Percona Monitoring and Management (PMM) para configurar el cliente (`pmm-client`).
    
3. **`--server-insecure-tls`**  
    Permite la conexión con el servidor PMM aunque tenga un certificado TLS no válido (autofirmado o inseguro).
    
4. **`--server-url=http://admin:admin@172.17.0.2:8443`**  
    Define la URL del servidor PMM, con usuario `admin` y contraseña `admin`, ubicado en `172.17.0.2`, puerto `8443`.  
    → Este es el servidor PMM al que se conectará el cliente.
    
5. **`172.17.0.4`**  
    Especifica la IP del host que se va a registrar en PMM (probablemente otro contenedor o máquina con una base de datos).
    
6. **`container ps-dk-container`**  
    Registra un servicio con el nombre `ps-dk-container`, indicando que el objetivo es un contenedor.
    
7. **`--force`**  
    Fuerza la configuración, sobrescribiendo cualquier configuración previa.

Check status

```shell
docker exec -t pmm-client pmm-admin status
```

Obtener la IP de Percona Server for Mysql
```shell
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ps-mysql
```

Añadir el servicio de Mysql en el contenedor de PMMClient con Percona PMM

```shell
docker exec pmm-client pmm-admin add mysql --username=root --password=root --host=172.17.0.3 --port=3306 --query-source=perfschema mysql-db
```

---

## Configuración de MongoDB con Docker

### 1. Iniciar un contenedor de MongoDB con Percona
```sh
docker run -d --name ps-mongo -p 27018:27017 --restart always percona/percona-server-mongodb:8.0
```
- **`-d`**: Ejecuta el contenedor en modo demonio (en segundo plano).
- **`--name ps-mongo`**: Asigna el nombre `ps-mongo` al contenedor.
- **`-p 27018:27017`**: Mapea el puerto local `27018` al puerto interno `27017` de MongoDB.
- **`--restart always`**: Configura el contenedor para reiniciarse siempre que se detenga o falle.
- **`percona/percona-server-mongodb:8.0`**: Usa la imagen de Percona Server for MongoDB versión 8.0.

### 2. Acceder al contenedor
```sh
docker exec -it ps-mongo bash
```
- **`docker exec`**: Ejecuta un comando dentro de un contenedor en ejecución.
- **`-it`**: Permite la interacción con una terminal.
- **`ps-mongo`**: Nombre del contenedor en el que se ejecutará el comando.
- **`bash`**: Inicia una sesión de terminal dentro del contenedor.

### 3. Iniciar el cliente de MongoDB
```sh
mongosh
```
- Inicia la shell interactiva de MongoDB (`mongosh`).

### 4. Cambiar al contexto de administración
```sh
use admin
```
- Cambia a la base de datos `admin` para la configuración de usuarios y permisos.

### 5. Crear un usuario administrador
```sh
db.createUser({
    user: "admin",
    pwd: "admin", // o una contraseña segura
    roles: [
        { role: "userAdminAnyDatabase", db: "admin" },
        { role: "readWriteAnyDatabase", db: "admin" }
    ]
})
```
- Crea un usuario con nombre `admin` y contraseña `admin`.
- Asigna los roles:
  - `userAdminAnyDatabase`: Permiso para administrar usuarios en cualquier base de datos.
  - `readWriteAnyDatabase`: Permiso de lectura y escritura en cualquier base de datos.

### 6. Apagar MongoDB desde la shell
```sh
db.adminCommand({ shutdown: 1 })
```
- Cierra la instancia de MongoDB de manera segura.

### 7. Conectar con autenticación
```sh
mongosh -u admin -p admin --authenticationDatabase admin
```
- **`-u admin`**: Usuario `admin`.
- **`-p admin`**: Contraseña `admin`.
- **`--authenticationDatabase admin`**: Base de datos donde se encuentra el usuario de autenticación.

Este flujo permite iniciar y configurar un servidor MongoDB dentro de un contenedor Docker, agregar un usuario administrador y conectarse con autenticación.

