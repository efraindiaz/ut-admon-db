## 🧹 Instrucciones de limpieza de datos para reservas de hotel

### 1️⃣ Corregir la columna `bookingSource`
- 🔁 Unificar los valores que representan la misma fuente (por ejemplo: *booking.com*, *BOking*, *Booking* → `Booking.com`).
- 🧱 Estandarizar nombres de plataformas como `Airbnb`, `Facebook`, `Instagram`, `WhatsApp`, etc.

### 2️⃣ Normalizar la columna `emailConfirmed`
- ✅ Unificar todas las respuestas afirmativas (ej. *sí*, *yes*, *ok*, *y*, *confirmado*, etc.) bajo el valor: `Sí`.
- ❌ Unificar todas las respuestas negativas (ej. *no*, *n*, *NO*, cadenas vacías, etc.) bajo el valor: `No`.

### 3️⃣ Verificar coherencia de fechas (`arrivalDate` y `departureDate`)
- 📅 Validar que ambas fechas estén en formato correcto (`AAAA-MM-DD`).
- 🔎 Asegurar que `departureDate` siempre sea posterior a `arrivalDate`.

### 4️⃣ Calcular la columna `nights`
- ⏳ Crear una nueva columna que calcule automáticamente el número de noches entre `arrivalDate` y `departureDate`.

### 5️⃣ Analizar y descomponer la columna `extraInfo`
- 🧩 Validar que el contenido sea un JSON estructurado correctamente.
- 📊 Crear **tres nuevas columnas** a partir del JSON:
  - 💰 `price`: monto total de la reservación.
  - 🌐 `currency`: tipo de moneda (debe estandarizarse a `MXN` o `USD`).
  - 🏨 `room`: tipo de habitación (corregir inconsistencias como *delux*, *estandar*, etc.).

