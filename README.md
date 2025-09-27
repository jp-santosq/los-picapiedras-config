# 📂 Configuración de entornos — Los Picapiedras

Este directorio contiene los archivos de configuración en formato **JSON** para los distintos entornos de despliegue del proyecto **Los Picapiedras**.

## 📄 Archivos

- `development.json` → entorno local de desarrollo.
- `staging.json` → entorno de pruebas en un servidor local gestionado con **Coolify**.
- `production.json` → entorno productivo en **Oracle Cloud (OCI)**.

## 📑 Formato

Los archivos están en **JSON**.  

### Convenciones de nomenclatura
- **Variables principales**: `MAYÚSCULAS_CON_GUIONES_BAJOS`.
- **Objetos internos**: `snake_case` (ejemplo: `enable_new_ui`).
- **Valores**: strings entre comillas, numéricos sin comillas, booleanos `true`/`false`.

# 📑 Parámetros de configuración

### 🔹 Base de datos
- **`DB_HOST`** → Dirección o hostname del servidor de base de datos.  
  Ejemplo: `localhost` en desarrollo, `adb.us-ashburn-1.oraclecloud.com` en producción.

- **`DB_PORT`** → Puerto de conexión a la base de datos.  
  Por defecto `5432` para Postgres y `1522` para Oracle Autonomous Database.

- **`DB_NAME`** → Nombre de la base de datos.  
  Usado en desarrollo y staging con Postgres. Ejemplo: `picapiedras_dev`.

- **`DB_SERVICE`** → Nombre del servicio de Oracle Autonomous Database.  
  Usado en producción. Ejemplo: `picapiedras_high.adb.oraclecloud.com`.

- **`DB_USER`** → Usuario con permisos para conectarse a la base de datos.

- **`DB_PASSWORD`** → Contraseña del usuario de la base de datos.  
  ⚠️ En producción debe obtenerse desde **OCI Vault**, nunca en texto plano.

- **`WALLET_PATH`** → Ruta al **Oracle Wallet** (archivos de credenciales) usado para conexión segura con Autonomous Database.  
  Solo en producción.

---

### 🔹 Aplicación
- **`SERVER_PORT`** → Puerto en el que se ejecuta el backend (Spring Boot).  
  Generalmente `8080`.

- **`API_BASE_URL`** → URL base del backend usada por el frontend.  
  Ejemplo: `http://localhost:8080/api` en desarrollo o `https://los-picapiedras-prod.oci.example.com/api` en producción.

- **`JWT_SECRET`** → Clave secreta usada para firmar y validar tokens JWT.  
  ⚠️ En producción debe almacenarse en **OCI Vault**.

- **`LOG_LEVEL`** → Nivel de logs de la aplicación.  
  Valores típicos:  
  - `DEBUG` → Desarrollo.  
  - `INFO` → Staging.  
  - `WARN` → Producción.  
  - `ERROR` → Solo errores críticos.

---

### 🔹 Oracle Cloud (Producción)
- **`OCI_REGION`** → Región de despliegue en Oracle Cloud Infrastructure.  
  Ejemplo: `us-ashburn-1`, `mexico-city-1`.

- **`OCI_BUCKET`** → Nombre del bucket en **OCI Object Storage** usado para almacenar logs, respaldos o assets.

---

### 🔹 Feature Flags
- **`FEATURE_FLAGS`** → Objeto con banderas para activar/desactivar funcionalidades específicas:  
  - **`enable_new_ui`** → Activa la nueva interfaz gráfica.  
  - **`mock_external_services`** → Permite simular servicios externos (solo en desarrollo).  

