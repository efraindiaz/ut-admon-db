# Unidad I: Administración de Bases de Datos Relacionales

## Tema 01: Copias de Seguridad y Restauración

### 🔒 Concepto de Copias de Seguridad
Una copia de seguridad es un proceso para duplicar datos y protegerlos contra pérdidas, fallos del sistema o corrupción. Se realiza para garantizar la continuidad de las operaciones y la disponibilidad de la información.

### 🌐 Tipos de Copias de Seguridad
1. **Copia Completa:**
   - Incluye todos los datos y estructuras de la base de datos.
   - **Ventaja:** Fácil restauración.
   - **Desventaja:** Uso intensivo de espacio y tiempo.

2. **Copia Incremental:**
   - Solo copia los cambios realizados desde la última copia (completa o incremental).
   - **Ventaja:** Menor espacio y tiempo de ejecución.
   - **Desventaja:** Restauración más compleja.

3. **Copia Diferencial:**
   - Copia los cambios realizados desde la última copia completa.
   - **Ventaja:** Restauración más sencilla que la incremental.
   - **Desventaja:** Tamaño crece con el tiempo desde la última copia completa.

### 🔧 Comandos y Herramientas

#### **1. Copias de Seguridad con `mysqldump` (MySQL)**
Realiza un respaldo completo:
```bash
mysqldump -u [usuario] -p [nombre_base_datos] > respaldo_completo.sql
```
- **`-u [usuario]`**: Nombre del usuario de MySQL.
- **`-p`**: Solicita la contraseña.
- **`[nombre_base_datos]`**: Nombre de la base de datos a respaldar.

Para restaurar:
```bash
mysql -u [usuario] -p [nombre_base_datos] < respaldo_completo.sql
```

**Ejemplo con compresión:**
```bash
mysqldump -u root -p tienda | gzip > respaldo_completo.sql.gz
```

#### **2. Copias de Seguridad con `pg_dump` (PostgreSQL)**
Generar un respaldo en formato texto plano:
```bash
pg_dump -U [usuario] -d [nombre_base_datos] > respaldo_completo.sql
```

Generar un respaldo en formato binario:
```bash
pg_dump -U [usuario] -d [nombre_base_datos] -F c -f respaldo_completo.backup
```
- **`-F c`**: Genera el respaldo en formato personalizado.

Para restaurar:
```bash
pg_restore -U [usuario] -d [nombre_base_datos] respaldo_completo.backup
```

#### **3. Copias Binarias con MySQL**
Realiza una copia directa de los archivos binarios:
1. Detén el servicio de MySQL para evitar inconsistencias:
   ```bash
   sudo systemctl stop mysql
   ```
2. Copia el directorio de datos:
   ```bash
   cp -r /var/lib/mysql /ruta/respaldo/mysql_binario
   ```
3. Reinicia el servicio de MySQL:
   ```bash
   sudo systemctl start mysql
   ```

Para restaurar, copia los archivos respaldados al directorio de datos original.

### ✅ Protocolo de Restauración
1. Identificar el respaldo necesario:
   - Copia completa.
   - Incremental o diferencial (aplicar en orden).

2. Restaurar usando las herramientas adecuadas:
   - Para SQL, usa los comandos `mysql` o `pg_restore`.
   - Para binarios, reemplaza los archivos en el sistema de archivos.

3. Verificar la integridad de los datos restaurados mediante consultas o pruebas.

### 🔎 Escenarios sugeridos para Copias de Seguridad
- **Recuperación tras un fallo:** Utiliza una copia completa reciente seguida de incrementales.
- **Migración de servidor:** Realiza un respaldo completo y restauralo en el nuevo entorno.
- **Clonación para desarrollo:** Genera una copia completa para pruebas en entornos aislados.

### 🔢 Consejos de Mejora
- Automatiza las copias con cron jobs o herramientas específicas.
- Comprime los respaldos para ahorrar espacio.
- Cifra los respaldos sensibles con herramientas como OpenSSL:
  ```bash
  openssl enc -aes-256-cbc -salt -in respaldo.sql -out respaldo.sql.enc -k contraseña
  ```

### 📊 Resumen
Este tema introduce las bases de las copias de seguridad y restauración, destacando las herramientas principales y los procedimientos recomendados para garantizar la disponibilidad y consistencia de los datos.

---

