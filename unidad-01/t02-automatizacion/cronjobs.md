# AS05 CRONJOBS

## Creando una automatización para respaldar una base de datos en 5 pasos:

### Paso 1: Crear el script Bash para el respaldo de la base de datos

**Crear el archivo del script:**

Abre una terminal y crea un archivo nuevo para el script, por ejemplo, `respaldo_mysql.sh`:

```shell
nano respaldo_mysql.sh
```

**Escribir el script:**

El contenido del script debe ser algo así:

```shell
#!/bin/bash

# Variables
DB_USER="root"
DB_NAME="test"
DB_PASS="test"
BACKUP_DIR=~/Documents/Backups

# Crear un nombre de archivo único con la fecha
TIMESTAMP=$(date +"%Y%m%d_%H%M%S")
BACKUP_FILE="${BACKUP_DIR}/test_backup_${TIMESTAMP}.sql"

# Exportar la base de datos
mysqldump -u $DB_USER -p$DB_PASS $DB_NAME > $BACKUP_FILE

# Confirmación
echo "Respaldo creado: $BACKUP_FILE"
```

**Explicación:**
- `DB_USER`, `DB_PASS`, y `DB_NAME` son las credenciales y el nombre de la base de datos de MySQL.
- `BACKUP_DIR` es el directorio donde quieres que se guarden los respaldos.
- `FECHA` es una variable que captura la fecha y hora actual para que el archivo de respaldo tenga un nombre único.
- `mysqldump` es el comando que realiza el respaldo de la base de datos.

### Paso 2: Dar permisos de ejecución al script

En la terminal, da permisos de ejecución al script:

```shell
chmod +x [nombre_del_archivo].sh
```

### Paso 3: Configurar el cronjob para ejecutar el script automáticamente

 **Editar el crontab:**
Se requiere configurar un cronjob para que el script se ejecute automáticamente todos los días a las 5 AM. Abre el archivo del crontab con el siguiente comando:

```shell
crontab -e
```

**Agregar la línea al crontab:**

En el archivo de crontab, agrega la siguiente línea al final del archivo:

```shell
0 5 * * * /ruta/al/script/respaldo_mysql.sh >> /ruta/al/log/respaldo_mysql.log 2>&1
```

```shell
* * * * * ~/Documents/Backups/cron.sh >> ~/Documents/Backups/cron.log 2>&1
```


* * * * * Documents/Backups/cron.sh >> /Documents/Backups/cron.log 2>&1

### **Paso 4: Verificar el cronjob**

Para verificar que el cronjob se ha agregado correctamente, puedes usar el siguiente comando:

```
crontab -l
```

Deberías ver algo como:

```
0 5 * * * /ruta/al/script/respaldo_mysql.sh >> /ruta/al/log/respaldo_mysql.log 2>&1
```

### **Paso 5: Comprobar que todo funcione**

- **Probar manualmente el script**: Antes de confiar en que el cronjob lo ejecutará correctamente, prueba ejecutando el script manualmente:

```shell
./respaldo_mysql.sh
```

Asegúrate de que se genere el archivo de respaldo en el directorio que especificaste y que el archivo de log registre correctamente el resultado.

Comprobar el log**: Después de la primera ejecución automática, revisa el archivo de log (`respaldo_mysql.log`) para asegurarte de que el cronjob está funcionando sin errores.
