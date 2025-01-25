# AS05.1 Sintaxis del cronjob

#### Sintaxis general del cronjob:

La estructura básica de un cronjob en `crontab` es la siguiente:

```
* * * * * comando_a_ejecutar
| | | | |
| | | | +---- Día de la semana (0 - 6) (Domingo=0 o 7)
| | | +------ Mes (1 - 12)
| | +-------- Día del mes (1 - 31)
| +---------- Hora (0 - 23)
+------------ Minuto (0 - 59)
```

#### **1. Minuto (primer campo)**

Este campo determina el **minuto** exacto en que se ejecutará el cronjob, con un valor entre **0** y **59**.

- **Ejemplo:**
    - `0`: El cronjob se ejecutará en el minuto 0 de la hora (es decir, exactamente a la hora en punto).
    - `30`: El cronjob se ejecutará a los 30 minutos de la hora.
    - `*/5`: El cronjob se ejecutará cada 5 minutos (esto significa que se ejecutará a los minutos 0, 5, 10, 15, 20, ...).

#### **2. Hora (segundo campo)**

Este campo determina la **hora** del día en que se ejecutará el cronjob, con un valor entre **0** y **23**. El valor **0** es la medianoche (12:00 AM), y **23** es la última hora antes de la medianoche.

- **Ejemplo:**
    - `3`: El cronjob se ejecutará a las 3 AM.
    - `14`: El cronjob se ejecutará a las 2 PM (14:00).
    - `*/2`: El cronjob se ejecutará cada 2 horas (es decir, a las 0:00, 2:00, 4:00, 6:00, ...).

#### **3. Día del mes (tercer campo)**

Este campo determina el **día del mes** en que se ejecutará el cronjob, con un valor entre **1** y **31**. Si se usa un asterisco `*`, el cronjob se ejecutará todos los días del mes.

- **Ejemplo:**
    - `1`: El cronjob se ejecutará el primer día del mes.
    - `15`: El cronjob se ejecutará el día 15 de cada mes.
    - `*/10`: El cronjob se ejecutará cada 10 días del mes (1, 11, 21, ...).

#### **4. Mes (cuarto campo)**

Este campo determina el **mes** en que se ejecutará el cronjob, con un valor entre **1** y **12** (donde **1** es enero y **12** es diciembre). También puedes usar el nombre del mes en inglés (por ejemplo, `Jan`, `Feb`, `Mar`).

- **Ejemplo:**
    - `1`: El cronjob se ejecutará en enero.
    - `6`: El cronjob se ejecutará en junio.
    - `*/3`: El cronjob se ejecutará cada 3 meses (enero, abril, julio, octubre).

#### **5. Día de la semana (quinto campo)**

Este campo determina el **día de la semana** en que se ejecutará el cronjob, con un valor entre **0** y **6** (donde **0** o **7** representan domingo). También puedes usar el nombre del día en inglés (por ejemplo, `Mon`, `Tue`, `Wed`).

- **Ejemplo:**
    - `0` o `7`: El cronjob se ejecutará los domingos.
    - `1`: El cronjob se ejecutará los lunes.
    - `5`: El cronjob se ejecutará los viernes.
    - `*/2`: El cronjob se ejecutará cada 2 días de la semana (lunes, miércoles, viernes, ...).

#### **Combinaciones y ejemplos:**

- **Ejemplo 1:** `30 8 * * * comando`
    - Se ejecuta **todos los días a las 8:30 AM**.
    
- **Ejemplo 2:** `0 5 * * 1 comando`    
    - Se ejecuta **todos los lunes a las 5:00 AM**.
    
- **Ejemplo 3:** `*/10 2 * * * comando`
    - Se ejecuta **cada 10 minutos a partir de las 2:00 AM**, es decir, a las 2:00, 2:10, 2:20, ..., 2:50.
    
- **Ejemplo 4:** `0 0 1 * * comando`
    - Se ejecuta **el primer día de cada mes a la medianoche**.
    
- **Ejemplo 5:** `0 12 1 1 * comando`
    - Se ejecuta **el 1 de enero a las 12:00 PM (mediodía)**.
    - 

#### **Uso de los asteriscos (`*`) y rangos:**

- **Asterisco (`*`)**: Indica "todos" los valores posibles. Por ejemplo, `* * * * *` ejecuta el comando **cada minuto de cada hora de cada día**.
    
- **Rangos (`-`)**: Puedes especificar un rango de valores, como `1-5`, que se refiere a los días de la semana de lunes a viernes. Por ejemplo, `0 12 * * 1-5` ejecutará el comando **a las 12:00 PM de lunes a viernes**.
    
- **Combinación de rangos y pasos (`/`)**: Puedes usar un rango con un paso, por ejemplo `*/5`, que ejecutará el cronjob en intervalos de 5 unidades. Ejemplo:
    
    - `*/5 * * * *` ejecuta el cronjob **cada 5 minutos**.
    - `1-10/2 * * * *` ejecuta el cronjob **en los minutos 1, 3, 5, 7, 9** de cada hora.

