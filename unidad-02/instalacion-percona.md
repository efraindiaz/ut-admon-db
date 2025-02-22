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

Opcion 1

PMM Client dentro de Percona Server

1 - Acceder al contenedor
```bash
docker exec -it percona-server bash
```

2 - Instalar PMM Client
```bash
sudo apt update && apt install -y pmm2-client
```

3 - Configurar conexion
```shell
pmm-admin config --server-insecure-tls --server-url=http://localhost:3999
```

4 - Registra el servicio MySQL en PMM
```shell
pmm-admin add mysql --username=root --password=rootpassword --host=localhost --port=3306
```

Opcion 2

Contenedor para **PMM Client**

1 - Deplegar contenedor
```shell
docker run -d \
  --name pmm-client \
  --restart always \
  --network host \
  percona/pmm-client:3
```

2 - Configurar conexion
```shell
docker exec pmm-client pmm-admin config --server-insecure-tls --server-url=http://172.17.0.2:3999
```


```shell
docker exec pmm-client pmm-admin config --server-insecure-tls --server-url=http://161.35.232.12:3999
```

3 - Registrar servicio
```shell
docker exec pmm-client pmm-admin add mysql --username=root --password=rootpass --host=percona-server --port=3306
```

```shell
pmm-admin config --server-insecure-tls --server-url=https://admin:admin@X.X.X.X:443
```

  docker pull percona/pmm-client:3
  
```shell
  PMM_SERVER=172.17.0.2:8443
  docker run \
  --name pmm-client \
  -e PMM_AGENT_SERVER_ADDRESS=${PMM_SERVER} \
  -e PMM_AGENT_SERVER_USERNAME=admin \
  -e PMM_AGENT_SERVER_PASSWORD=admin \
  -e PMM_AGENT_SERVER_INSECURE_TLS=1 \
  -e PMM_AGENT_SETUP=1 \
  -e PMM_AGENT_CONFIG_FILE=config/pmm-agent.yaml \
  -v pmm-client-data:/srv \
  percona/pmm-client:3
  ```


  docker exec -t pmm-client pmm-admin status

---

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

Percona Server Container IP

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

Check status

```shell
docker exec -t pmm-client pmm-admin status
```


Register your client nodes with PMM Server.

```shell
docker exec pmm-client pmm-admin config --server-insecure-tls --server-url=https://admin:admin@172.17.0.2:8443 --force
```

- `X.X.X.X` is the address of your PMM Server.
- `443` is the default port number.
- `admin`/`admin` is the default PMM username and password. This is the same account you use to log into the PMM user interface, which you had the option to change when first logging in.

```shell
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ps-mysql
```

Add the Mysql service to Percona PMM

```shell
docker exec pmm-client pmm-admin add mysql --username=root --password=root --host=172.17.0.3 --port=3306 --service-name=mysql-db
```

Some commands to fix errors adding the mysql service

```shell
docker exec -it ps-mysql ls -lah /var/lib/mysql/
```

```shell
docker exec -it ps-mysql touch /var/lib/mysql/mysql-slow.log
```

```shell
docker exec -it ps-mysql chmod 666 /var/lib/mysql/mysql-slow.log
```

```shell
docker exec -it pmm-client pmm-admin add mysql --username=root --password=root --host=172.17.0.3 --port=3306 --query-source=slowlog --slow-log=/var/lib/mysql/mysql-slow.log
```

```shell
docker restart pmm-client
```

