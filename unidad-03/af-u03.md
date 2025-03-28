# **📌 Actividad: Creación, Limpieza y Normalización de Datos con OpenRefine y MySQL**  

## **🎯 Objetivo:**  
Cada equipo diseñará un **caso de uso** con datos desordenados e inconsistentes, aplicará técnicas de **limpieza y normalización** en OpenRefine y documentará el proceso en un **reporte** y una **presentación en PowerPoint**.  

---

## **📌 Parte 1: Creación del Set de Datos**  

### **🔹 Instrucciones**  

1️⃣ **Definir un contexto y objetivo de limpieza**  
   - Elijan un caso de uso realista donde la limpieza de datos sea necesaria (ej. reservas de hotel, gestión de pacientes, ventas en línea, etc.).  
   - Definan **por qué** es importante limpiar estos datos en su contexto.  

2️⃣ **Diseñar la base de datos**  
   - Debe incluir **mínimo 3 tablas**.  
   - Cada tabla debe tener **mínimo 4 columnas con errores intencionales** (pero pueden agregar más columnas si lo consideran necesario).  
   - Agreguen **mínimo 100 registros por tabla** que contengan errores intencionales.  

3️⃣ **Generación de los datos inconsistentes**  
   - Pueden **crear los datos manualmente** o **asistirse con herramientas de inteligencia artificial** para generar registros con inconsistencias.  
   - Cada tabla debe contener **datos inconsistentes**, por ejemplo:  
     - **Errores de formato** (fechas en distintos formatos, números con símbolos no deseados).  
     - **Datos duplicados** (registros repetidos con ligeras variaciones en nombres, espacios extra).  
     - **Valores incompletos** (campos vacíos o con datos faltantes).  
     - **Errores de digitación** (nombres mal escritos, números de teléfono incorrectos).  
     - **Separación de columnas** (ej. nombres completos en una sola columna en lugar de nombre y apellido separados).  

**Ejemplo:**  
📌 **Caso: Gestión de Pacientes en un Hospital**  

| ID | Nombre Completo  | Fecha de Nacimiento | Teléfono       | Diagnóstico     |  
|----|----------------|-------------------|---------------|---------------|  
| 1  | Juan Pérez    | 15-08-1990        | +52 55-1234-5678  | Hipertensión |  
| 2  | Maria G.      | 1992/04/30        | 55123 45678   | Diabetes |  
| 3  | Juan Perez    | 1990-08-15        | +52 1 55 1234 5678 | Hipertension  |  

---

## **📌 Parte 2: Proceso de Limpieza en OpenRefine**  
Cada equipo debe realizar las siguientes acciones en OpenRefine:  

1️⃣ **Importar los datos en OpenRefine**.  
2️⃣ **Identificar errores y aplicar transformaciones**, usando expresiones GREL cuando sea necesario.  
3️⃣ **Eliminar duplicados** y corregir valores inconsistentes.  
4️⃣ **Unificar formatos de fechas, números y nombres**.  
5️⃣ **Separar o unir columnas cuando sea necesario**.  
6️⃣ **Exportar los datos limpios y normalizados**.  

---

## **📌 Parte 3: Reporte del Proceso**  

Cada equipo debe generar un **documento en PDF** que contenga:  

📌 **1. Contexto del set de datos y justificación**  
- Describan el caso de uso elegido y expliquen por qué es importante limpiar los datos.  

📌 **2. Capturas de pantalla del proceso en OpenRefine**  
- **Antes y después de cada transformación.**  
- Cada imagen debe incluir una **descripción clara** y, si aplica, la **expresión GREL usada**.  

📌 **3. Explicación de cada paso realizado**  
- Cómo identificaron los errores.  
- Qué técnicas de limpieza usaron.  
- Cómo transformaron los datos.  

📌 **4. Resultados y conclusiones**  
- Comparación de los datos antes y después de la limpieza.  
- Reflexión sobre la importancia de la normalización de datos.  

---

## **📌 Parte 4: Presentación en PowerPoint** 🎤  

Cada equipo deberá presentar su proceso en **una exposición de almenos 5 minutos**, usando una presentación con:  

📌 **1. Introducción**  
- Caso de uso y contexto del set de datos.  
- Ejemplos de errores encontrados.  

📌 **2. Proceso de limpieza en OpenRefine**  
- Capturas de pantalla con explicaciones de cada paso.  
- Transformaciones aplicadas (incluyendo expresiones GREL).  

📌 **3. Comparación de antes y después**  
- Mostrar diferencias entre los datos iniciales y los datos normalizados.  

📌 **4. Conclusión y aprendizajes**  
- Reflexión sobre la importancia de la calidad de los datos.  

---

