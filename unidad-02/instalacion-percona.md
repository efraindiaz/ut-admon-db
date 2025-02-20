# Instalación Percona

Percona PMM Server
Percona Server
Percona Client
Percona Server for MongoDB
Percona PMM Server
Image

docker pull percona/pmm-server:3
Volume

docker volume create pmm-data
Contenedor

docker run --detach --restart always --publish 3999:8443 -v pmm-data:/srv --name pmm-server percona/pmm-server:3
Percona Server For MySQL
Contenedor

docker run -d \
  --name ps-mysql \
  -e MYSQL_ROOT_PASSWORD=rootpass \
  -e MYSQL_DATABASE=ps_employees \
  -e MYSQL_USER=dev \
  -e MYSQL_PASSWORD=devpass \
  -p 3998:3306 \
  --restart unless-stopped \
  percona/percona-server:latest
Validación

docker exec -it ps-mysql bash
Conexión BD*

docker exec -it ps-mysql mysql -u root -p
PMM Client
Opcion 1

PMM Client dentro de Percona Server

1 - Acceder al contenedor

docker exec -it percona-server bash
2 - Instalar PMM Client

sudo apt update && apt install -y pmm2-client
3 - Configurar conexion

pmm-admin config --server-insecure-tls --server-url=http://localhost:3999
4 - Registra el servicio MySQL en PMM

pmm-admin add mysql --username=root --password=rootpassword --host=localhost --port=3306
Opcion 2

Contenedor para PMM Client

1 - Deplegar contenedor

docker run -d \
  --name pmm-client \
  --restart always \
  --network host \
  percona/pmm-client:latest
2 - Configurar conexion

docker exec pmm-client pmm-admin config --server-insecure-tls --server-url=http://localhost:3999
3 - Registrar servicio

docker exec pmm-client pmm-admin add mysql --username=root --password=rootpassword --host=percona-server --port=3306
