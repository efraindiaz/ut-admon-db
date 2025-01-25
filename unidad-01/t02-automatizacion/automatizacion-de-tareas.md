# S05 Automatización de tareas

La automatización de tareas es una estrategia clave para optimizar procesos, ahorrar tiempo y reducir errores humanos en la administración de sistemas y bases de datos.

---

## 🕒 Conceptos y beneficios de la automatización

- **¿Qué es la automatización de tareas?**
  La automatización consiste en programar actividades repetitivas para que se ejecuten automáticamente sin intervención humana.

- **Beneficios principales:**
  - Ahorro de tiempo y recursos.
  - Reducción de errores humanos.
  - Incremento en la consistencia y confiabilidad.
  - Mejora en la productividad del equipo.

---

## 🔄 Tareas automatizadas comunes

1. **Respaldos automáticos:**
   - Programar respaldos periódicos de bases de datos para garantizar la recuperación ante fallos.
   - Ejemplo: Copias completas, diferenciales o incrementales.

2. **Mantenimiento de índices:**
   - Reorganización y reconstrucción de índices en bases de datos para optimizar el rendimiento de las consultas.

3. **Limpieza de datos:**
   - Eliminación de datos obsoletos o innecesarios.
   - Archivar datos históricos para mejorar el rendimiento del sistema.

---

## 🛠️ Herramientas para programar tareas

### Cron y scripts en Linux
- **Cron:**
  Una utilidad en sistemas Unix/Linux para programar tareas periódicas.
  - Archivo de configuración: `crontab`.
  - Sintaxis de programación:
    ```
    * * * * * comando_a_ejecutar
    # Minuto, Hora, Día del mes, Mes, Día de la semana
    ```
  - Ejemplo: Respaldar una base de datos MySQL cada día a las 2:00 AM:
    ```bash
    0 2 * * * mysqldump -u usuario -p contraseña nombre_bd > /ruta/respaldo.sql
    ```


- **Scripts en Bash:**
  - Útiles para combinar múltiples comandos en un solo flujo automatizado.
  - Ejemplo de script para limpieza de archivos temporales:
    ```bash
    #!/bin/bash
    find /tmp -type f -mtime +7 -exec rm -f {} \;
    echo "Archivos temporales eliminados."
    ```

### Creando Scripts

Los archivos `.sh` y `.bat` son formatos de script utilizados para automatizar tareas, pero tienen diferencias significativas debido a los sistemas operativos en los que se ejecutan.

**Archivos .sh (Shell Script):**

- **Sistema operativo:** Principalmente asociados con sistemas operativos tipo Unix (Linux, macOS).
- **Intérprete:** Son interpretados por un shell, como Bash, Zsh o Ksh.
- **Sintaxis:** Utilizan una sintaxis específica de Unix, con comandos como `cd`, `ls`, `grep`, etc.
- **Funcionalidad:** Se utilizan para una amplia gama de tareas, desde automatización de tareas simples hasta scripts complejos para administración de sistemas.
- **Portabilidad:** Generalmente son más portables entre diferentes distribuciones de Linux debido a la estandarización de los shells.

**Archivos .bat (Batch File):**

- **Sistema operativo:** Exclusivos de sistemas operativos Windows.
- **Intérprete:** Son interpretados por el intérprete de comandos de Windows (cmd.exe).
- **Sintaxis:** Utilizan comandos específicos de Windows, como `dir`, `copy`, `del`, etc.
- **Funcionalidad:** Se utilizan para automatizar tareas en Windows, como crear directorios, copiar archivos, ejecutar programas, etc.
- **Limitaciones:** Comparados con los scripts Bash, suelen ser menos potentes y flexibles.



