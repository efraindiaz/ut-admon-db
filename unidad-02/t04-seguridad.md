# **Tema 4: Administración de Seguridad en MongoDB**

## **1. Configuración de Usuarios y Permisos 🔐**

MongoDB permite gestionar la seguridad mediante autenticación y control de acceso basados en roles.

### **1.1 Creación de un Usuario en MongoDB**

Los usuarios deben crearse dentro de la base de datos `admin` para tener permisos globales.

#### **Ejemplo: Crear un usuario administrador**

```javascript
use admin
db.createUser({
  user: "admin",
  pwd: "secure_password",
  roles: [ { role: "root", db: "admin" } ]
})
```

### **1.2 Crear un Usuario con Permisos Específicos**

```javascript
db.createUser({
  user: "r_user",
  pwd: "passwordabc123",
  roles: [ { role: "read", db: "my_db" } ]
})
```

Este usuario solo podrá leer datos de `my_db`.

### **1.3 Roles Predefinidos en MongoDB**

- `read` → Permite solo lectura en la base de datos.
- `readWrite` → Permite lectura y escritura.
- `dbAdmin` → Permite administración de índices y estadísticas.
- `userAdmin` → Permite gestionar usuarios.
- `root` → Acceso total a todas las bases de datos.

# **2. Restricciones de Acceso Local y Remoto 🔬**

MongoDB, por defecto, solo permite conexiones locales (`localhost`) para mejorar la seguridad. Para aceptar conexiones remotas, es necesario modificar la configuración y ajustar el firewall en el sistema operativo.

---

## **2.1 Configuración de Acceso Local**

Por defecto, MongoDB escucha solo en `127.0.0.1`. Para verificarlo:

- **Linux/macOS:**
    
    ```bash
    netstat -tulnp | grep mongod
    ```
    
- **Windows (PowerShell como Administrador):**
    
    ```powershell
    netstat -ano | findstr :27017
    ```
    

Si ves una línea similar a esta, significa que MongoDB solo acepta conexiones locales:

```
tcp  0  0 127.0.0.1:27017  0.0.0.0:*  LISTEN  1234/mongod
```

---

## **2.2 Habilitar Acceso Remoto**

Para permitir conexiones remotas, edita el archivo de configuración de MongoDB (`mongod.conf`):

- **Linux/macOS:**
    
    ```bash
    sudo nano /etc/mongod.conf
    ```
    
- **Windows (PowerShell como Administrador):**
    
    ```powershell
    notepad "C:\\Program Files\\MongoDB\\Server\\6.0\\bin\\mongod.cfg"
    ```
    

Modifica la sección `net:` para permitir accesos remotos:

```yaml
net:
  bindIp: 0.0.0.0  # Permite conexiones desde cualquier IP
  port: 27017
```

⚠️ **Nota:** En un entorno de producción, especifica las IPs permitidas en lugar de `0.0.0.0` por razones de seguridad, por ejemplo:

```yaml
bindIp: 127.0.0.1,192.168.1.100
```

Guarda los cambios y **reinicia MongoDB**:

- **Linux/macOS:**
    
    ```bash
    sudo systemctl restart mongod
    ```
    
- **Windows (CMD/PowerShell como Administrador):**
    
    ```powershell
    net stop MongoDB
    net start MongoDB
    ```
    

Para verificar que MongoDB ahora acepta conexiones en todas las IPs:

```bash
netstat -tulnp | grep 27017  # Linux/macOS
```

```powershell
netstat -ano | findstr :27017  # Windows
```

---

## **2.3 Configuración de Firewall**

Si el servidor tiene un firewall activo, se debe permitir el tráfico en el puerto **27017**.

### **🖥️ Windows (Firewall de Windows)**

1. Abre **PowerShell** como Administrador.
2. Ejecuta el siguiente comando para permitir conexiones en el puerto 27017:
    
    ```powershell
    New-NetFirewallRule -DisplayName "MongoDB" -Direction Inbound -Protocol TCP -LocalPort 27017 -Action Allow
    ```
    
3. Para verificar la regla:
    
    ```powershell
    Get-NetFirewallRule -DisplayName "MongoDB"
    ```
    

### **🐧 Linux (Ubuntu/Debian con UFW)**

```bash
sudo ufw allow 27017/tcp
sudo ufw reload
```

Para **listar los puertos abiertos** en **UFW**:

```bash
sudo ufw status verbose
```

### **Linux (CentOS/RHEL con firewalld)**

```bash
sudo firewall-cmd --zone=public --add-port=27017/tcp --permanent
sudo firewall-cmd --reload
```

Para **listar los puertos abiertos** en **firewalld**:

```bash
sudo firewall-cmd --list-ports
```

### **🍏 macOS (Firewall)**

1. Ve a **Preferencias del Sistema** → **Seguridad y Privacidad** → **Firewall**.
2. Asegúrate de que el firewall está activado.
3. Agrega MongoDB a la lista de aplicaciones permitidas o usa el siguiente comando para abrir el puerto:
    
    ```bash
    sudo pfctl -f /etc/pf.conf
    echo "pass in proto tcp from any to any port 27017" | sudo pfctl -Ef -
    ```
    

Para **listar las reglas activas** en el firewall de **macOS**:

```bash
sudo pfctl -sr
```

### **2.4 Conexión Remota desde un Cliente MongoDB**

Para conectarse de manera remota a MongoDB desde otro equipo:

```bash
mongo --host SERVER_IP --port 27017 -u "admin" -p "secure_password" --authenticationDatabase "admin"
```

---
## **3. Puntos importantes a tener presente**

- La seguridad en MongoDB se gestiona con usuarios y roles.
- Es importante restringir el acceso remoto si no es necesario.
- Configurar un firewall es clave para evitar accesos no autorizados.
