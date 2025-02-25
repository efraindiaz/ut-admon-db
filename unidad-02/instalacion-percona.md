# Instalación de Percona

- Percona PMM Server
- Percona Server
- Percona Client
- Percona Server for MongoDB

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

Register your client nodes with PMM Server.

```shell
docker exec pmm-client pmm-admin config --server-insecure-tls --server-url=https://admin:admin@172.17.0.2:8443 --force
```

- `X.X.X.X` is the address of your PMM Server.
- `443` is the default port number.
- `admin`/`admin` is the default PMM username and password. This is the same account you use to log into the PMM user interface, which you had the option to change when first logging in.

Check status

```shell
docker exec -t pmm-client pmm-admin status
```

Obtener la IP de Percona Server for Mysql
```shell
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ps-mysql
```

Add the Mysql service to Percona PMM

```shell
docker exec pmm-client pmm-admin add mysql --username=root --password=root --host=172.17.0.3 --port=3306 --service-name=mysql-db
```

Registrar el servicio de Mysql con Percona PMM

```shell
docker exec pmm-client pmm-admin add mysql --username=root --password=root --host=172.17.0.3 --port=3306 --query-source=perfschema mysql-db
```

---

MongoDB

```shell
docker run -d --name ps-mongo -p 27017:27017 --restart always percona/percona-server-mongodb:8.0
```

```bash
docker exect -it ps-mongo bash
```

```bash
mongosh
```

```bash
use admin
```

```bash
db.createUser(
{
user: "admin",
pwd: "admin", // or cleartext password
roles: [
{ role: "userAdminAnyDatabase", db: "admin" },
{ role: "readWriteAnyDatabase", db: "admin" }
]
}
)
```

```bash
db> db.adminCommand( { shutdown: 1 } )
```
