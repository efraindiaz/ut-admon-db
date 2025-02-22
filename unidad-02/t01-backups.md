# Copias de Seguridad y Restauración en Bases de Datos No Relacionales

La copia de seguridad y restauración de bases de datos no relacionales es crucial para garantizar la integridad y disponibilidad de los datos en caso de fallos, errores humanos o ataques cibernéticos. A continuación, se detallan estrategias, herramientas y protocolos esenciales.

## 🔒 Estrategias para Bases No Relacionales

### 📌 Copias de Seguridad Completas

- Se realiza una copia de toda la base de datos.
- Ideal para sistemas pequeños o bases de datos críticas.
- Puede requerir una gran cantidad de almacenamiento.

**Ejemplo de Backup Completo en MongoDB:**

```bash
mongodump --host localhost --port 27017 --db mydatabase --out /backups/full_backup
```

### 📌 Copias de Seguridad Incrementales

- Solo se copian los datos que han cambiado desde la última copia de seguridad.
- Optimiza el tiempo y el almacenamiento necesario.
- Puede necesitar un proceso de restauración más complejo.

### 📌 Copias de Seguridad Diferenciales

- Copia los cambios realizados desde la última copia completa.
- Útil para encontrar un equilibrio entre tiempo y espacio de almacenamiento.

### 📌 Copias de Seguridad en Tiempo Real

- Se mantienen registros en tiempo real mediante mecanismos de replicación.
- Ideal para sistemas críticos con baja tolerancia a la pérdida de datos.
- Puede requerir infraestructura adicional para mantener múltiples copias en sincronización.

## ⚙️ Herramientas y Protocolos para Respaldos y Restauraciones

### 🔧 Herramientas Comunes

- **MongoDB Tools:** Incluye `mongodump` y `mongorestore` para respaldos y restauraciones.
- **Percona Backup for MongoDB:** Herramienta optimizada para respaldos eficientes y seguros.
- **Mongobackup:** Herramienta de terceros para operaciones programadas.
- **Amazon DynamoDB Backup & Restore:** Servicio administrado para copias de seguridad automáticas y restauraciones en bases de datos NoSQL en AWS.
- **Cassandra Snapshot Backup:** Para bases de datos Cassandra, se usan snapshots de nodos individuales.

## 🔄 Protocolos y Buenas Prácticas

### 🤖 Automatización

Es recomendable programar respaldos automáticos para evitar la pérdida de información importante.

**Ejemplo de cron job diario a las 2 AM:**

```bash
0 2 * * * mongodump --db mydatabase --out /backups/$(date +\%Y-\%m-\%d)
```

### 🔐 Cifrado de Datos

Es fundamental proteger las copias de seguridad con cifrado:

- Usar **TLS** para la transferencia de datos.
- Almacenar los respaldos en formatos cifrados (AES-256, GPG, etc.).

**Ejemplo de respaldo cifrado con OpenSSL:**

```bash
tar -cvzf - /backups/full_backup | openssl enc -aes-256-cbc -e -out backup.tar.gz.enc
```

### 🧪 Pruebas Periódicas de Restauración

Realizar pruebas regulares garantiza la validez y disponibilidad de las copias de seguridad. Sin pruebas, un backup puede resultar inservible en el momento de restauración.

**Ejemplo de verificación de integridad de un respaldo MongoDB:**

```bash
mongorestore --dryRun --host localhost --port 27017 --db test_restore /backups/full_backup/mydatabase
```

### 📜 Política de Retención de Datos

Definir períodos de retención basados en requisitos regulatorios y operativos:

- **Diarias:** Mantener copias de los últimos 7 días.
- **Semanales:** Conservar al menos 4 semanas.
- **Mensuales:** Mantener copias de los últimos 6-12 meses.

## 🛠️ Ejemplo de Restauración en MongoDB

**Restauración de una copia completa:**

```bash
mongorestore --host localhost --port 27017 --db mydatabase /backups/full_backup/mydatabase
```

**Restauración de una colección específica:**

```bash
mongorestore --host localhost --port 27017 --db mydatabase --collection users /backups/full_backup/mydatabase/users.bson
```

Este proceso garantiza que la base de datos pueda ser recuperada en su estado exacto al momento del respaldo.
