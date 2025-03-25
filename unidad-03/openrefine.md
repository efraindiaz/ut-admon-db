# 📊 Introducción a OpenRefine

## 🧐 ¿Qué es OpenRefine?

OpenRefine es una herramienta de código abierto utilizada para la limpieza y transformación de datos. Permite manipular grandes conjuntos de datos de manera eficiente, facilitando la detección y corrección de errores, estandarización de formatos y exploración de datos.

### 🌍 Contexto de la Herramienta

OpenRefine fue originalmente desarrollado por Google bajo el nombre de "Google Refine" y, posteriormente, se convirtió en un proyecto independiente de código abierto. Es especialmente utilizado en ciencia de datos, periodismo de datos y gestión de bases de datos para mejorar la calidad de la información.

---

## 🏆 Casos de Uso

1. **Limpieza de Datos** 🧹
    
    - Identificación y eliminación de duplicados.
    - Corrección de valores inconsistentes (Ejemplo: "México", "Mexico", "MEX").
    - Eliminación de caracteres especiales y espacios en blanco innecesarios.
2. **Transformación de Datos** 🔄
    
    - Convertir datos a diferentes formatos.
    - Aplicar reglas para modificar valores de manera automática.
    - Separación o combinación de columnas.
3. **Exploración y Análisis de Datos** 🔍
    
    - Visualización rápida de patrones y distribuciones.
    - Identificación de errores y anomalías en los datos.
4. **Enriquecimiento de Datos** 📈
    
    - Conexión con servicios externos como Wikidata o APIs para completar información faltante.

---

## 🚀 Alcance de OpenRefine

- OpenRefine **no es** una base de datos ni un reemplazo de herramientas como Excel o SQL.
- Es ideal para **preparar datos** antes de importarlos a un sistema de base de datos o herramienta de análisis.
- Puede trabajar con formatos como **CSV, TSV, JSON, Excel y SQL**.
- Funciona localmente en el navegador sin necesidad de conexión a internet.

---

## 🛠 Componentes y Uso de OpenRefine

### 📂 1. Creación de un Proyecto

- Puedes importar archivos desde CSV, JSON, SQL, etc.
- Permite visualizar los datos en una interfaz tabular.

### 🔍 2. Filtrado y Exploración

- **Facetas**: Permiten agrupar datos similares para identificar inconsistencias.
- **Filtros**: Ayudan a buscar valores específicos en las columnas.
- **Expresiones Regulares**: Se pueden usar para encontrar patrones de datos.

### ✨ 3. Transformación de Datos

- **Operaciones en columnas**: Reemplazo de valores, conversión de tipos de datos, etc.
- **Clustering**: Une valores similares automáticamente.
- **Expresiones GREL**: Un lenguaje especial para manipular datos (similar a Excel o SQL).

### 🔄 4. Exportación de Datos

- Se puede exportar en CSV, JSON, Excel, SQL o conectarse con bases de datos.

---

## 🎯 Conclusión

OpenRefine es una herramienta poderosa para la **gestión de la calidad de datos**, permitiendo limpiar, transformar y analizar grandes volúmenes de información de manera sencilla y eficiente. Su uso es fundamental en cualquier disciplina que requiera datos confiables.

---

## 🔗 Recursos Adicionales

- Sitio oficial: [https://openrefine.org/](https://openrefine.org/)
- Documentación: [https://docs.openrefine.org/](https://docs.openrefine.org/)
- Tutoriales en video: [https://www.youtube.com/c/OpenRefine](https://www.youtube.com/c/OpenRefine)

## 🔹 **Expresiones**


OpenRefine usa **GREL (General Refine Expression Language)** como su lenguaje principal para manipular y transformar datos. Es un lenguaje expresivo y flexible que permite limpiar, modificar y analizar datos dentro de OpenRefine.

---

## 🔹 **¿Qué es GREL?**

GREL (**General Refine Expression Language**) es un lenguaje de expresiones en OpenRefine utilizado para:

- Transformar datos en celdas.
- Filtrar y dividir contenido.
    
- Aplicar operaciones matemáticas y de texto.
    
- Realizar conversiones entre tipos de datos.
    

GREL se usa en la pestaña **"Transform"** dentro de OpenRefine, cuando se editan celdas de manera masiva.

---

## 🔹 **Funciones comunes en GREL**

### 📌 **Funciones de Texto**

|**Función**|**Descripción**|**Ejemplo**|**Resultado**|
|---|---|---|---|
|`value.toUppercase()`|Convierte a mayúsculas|`"hola".toUppercase()`|`"HOLA"`|
|`value.toLowercase()`|Convierte a minúsculas|`"Hola".toLowercase()`|`"hola"`|
|`value.trim()`|Elimina espacios en blanco|`" Hola ".trim()`|`"Hola"`|
|`value.length()`|Devuelve la longitud de un string|`"Hola".length()`|`4`|
|`value.replace("a", "o")`|Reemplaza caracteres|`"banana".replace("a", "o")`|`"bonono"`|

---

### 📌 **Funciones de División y Unión de Datos**

|**Función**|**Descripción**|**Ejemplo**|**Resultado**|
|---|---|---|---|
|`value.split(",")`|Divide un string en una lista|`"manzana,pera".split(",")`|`["manzana", "pera"]`|
|`value.join(",")`|Une elementos de una lista|`["uno", "dos"].join("-")`|`"uno-dos"`|

---

### 📌 **Funciones de Tipo de Dato**

|**Función**|**Descripción**|**Ejemplo**|**Resultado**|
|---|---|---|---|
|`toNumber(value)`|Convierte en número|`toNumber("123")`|`123`|
|`toString(value)`|Convierte en texto|`toString(123)`|`"123"`|
|`isNull(value)`|Verifica si es nulo|`isNull(null)`|`true`|

---

### 📌 **Condiciones y Expresiones Lógicas**

| **Función**                                         | **Descripción**        | **Ejemplo**             | **Resultado** |
| --------------------------------------------------- | ---------------------- | ----------------------- | ------------- |
| `if(condición, valor_si_verdadero, valor_si_falso)` | Evalúa una condición   | `if(5 > 3, "Sí", "No")` | `"Sí"`        |
| `isBlank(value)`                                    | Verifica si está vacío | `isBlank("")`           | `true`        |
| `or(true, false)`                                   | Operador OR            | `or(true, false)`       | `true`        |
| `and(true, false)`                                  | Operador AND           | `and(true, false)`      | `false`       |

---

