# Node & Express Web App

Aplicación web backend desarrollada con **Node.js** y **Express** como proyecto integrador del bootcamp Alkemy (Módulos 6, 7 y 8).

Docente: Sabina Romero

---

## Tecnologías utilizadas

- **Node.js** v18+
- **Express.js** v4
- **dotenv** — variables de entorno
- **nodemon** — recarga automática en desarrollo

---

## Estructura del proyecto

```
node-express-webapp/
├── index.js              # Punto de entrada del servidor
├── package.json
├── .env                  # Variables de entorno (no se sube a GitHub)
├── .env.example          # Plantilla de variables de entorno
├── .gitignore
├── routes/
│   └── router.js         # Enrutador central (conectado con app.use)
├── controllers/
│   ├── homeController.js  # Lógica de la ruta GET /
│   └── statusController.js# Lógica de la ruta GET /status
├── middlewares/
│   └── logger.js         # Registra visitas en logs/log.txt
├── public/
│   └── styles.css        # Archivos estáticos servidos por Express
├── logs/
│   └── log.txt           # Generado automáticamente al ejecutar el servidor
└── utils/                # Utilidades reutilizables (disponible para módulos 7-8)
```

### Decisiones de diseño

- **`index.js` como archivo principal:** Se eligió este nombre por convención del ecosistema Node.js. Es el archivo que Node y npm resuelven automáticamente como punto de entrada (`"main"` en `package.json`), lo que facilita que cualquier desarrollador que clone el repositorio entienda dónde arranca la aplicación.

- **Router externo (`routes/router.js`):** Se separó el enrutamiento del archivo principal usando `app.use("/", router)`. Esto mantiene `index.js` limpio y permite agregar nuevos grupos de rutas fácilmente (e.g., `/api/users`) al escalar en los módulos 7 y 8.

- **Carpeta `/utils`:** Incluida desde el inicio para anticipar la escalabilidad. Aquí se agregarán helpers reutilizables (formateo de respuestas, validaciones, etc.) en las siguientes entregas.

- **`/public` para archivos estáticos:** Se usó `express.static()` apuntando a esta carpeta. Se eligió no usar motor de plantillas en esta etapa para mantener el enfoque en los conceptos base de Express; EJS será considerado en módulos siguientes si se requiere contenido dinámico del servidor.

---

## Requisitos del sistema

- Node.js **v18 o superior**
- npm v9+

Verificá tu versión con:

```bash
node -v
npm -v
```

---

## Instalación

```bash
# 1. Clonar el repositorio
git clone https://github.com/tu-usuario/node-express-webapp.git
cd node-express-webapp

# 2. Instalar dependencias
npm install

# 3. Configurar variables de entorno
cp .env.example .env
# Editá .env con tus valores si es necesario
```

---

## Ejecución

```bash
# Modo producción
npm start

# Modo desarrollo (con nodemon, recarga automática)
npm run dev
```

### ¿Por qué estos scripts?

- `npm start` → usa `node index.js`, el comando estándar para producción.
- `npm run dev` → usa `nodemon index.js`, que reinicia el servidor automáticamente ante cualquier cambio en el código durante el desarrollo.

---

## Rutas disponibles

| Método | Ruta      | Tipo de respuesta | Descripción                          |
|--------|-----------|-------------------|--------------------------------------|
| GET    | `/`       | HTML              | Página principal de bienvenida       |
| GET    | `/status` | JSON              | Estado actual del servidor           |

### Ejemplo de respuesta en `/status`

```json
{
  "status": "OK",
  "message": "El servidor está en funcionamiento",
  "data": {
    "app": "Node-Express-WebApp",
    "entorno": "development",
    "timestamp": "2025-01-15T14:30:00.000Z",
    "uptime": "42 segundos"
  }
}
```

---

## Archivos estáticos

La carpeta `/public` es servida automáticamente por Express mediante `express.static()`. Accedés a su contenido directamente desde la URL raíz:

- `http://localhost:3000/styles.css`

---

## Sistema de logging

Cada petición al servidor queda registrada en `logs/log.txt` con el siguiente formato:

```
[15/1/2025] [14:30:00] GET /
[15/1/2025] [14:30:05] GET /status
[15/1/2025] [14:30:10] GET /styles.css
```

El middleware `logger.js` usa `fs.appendFile()` para agregar líneas sin sobreescribir el historial. El archivo se crea automáticamente si no existe.

> **Nota:** `log.txt` está en `.gitignore` para no subir datos de uso al repositorio. La carpeta `logs/` se mantiene rastreada mediante un archivo `.gitkeep`.

---

## Reflexiones técnicas

Este módulo estableció los fundamentos del desarrollo backend con Node.js y Express. Los aprendizajes clave fueron:

- La diferencia entre Node puro (bajo nivel, manejo manual de rutas y respuestas) y Express (abstracción que simplifica enormemente el routing y los middlewares).
- El concepto de **middleware** como función intermediaria en el pipeline de peticiones, que permite modularizar comportamientos transversales como logging, autenticación y validación.
- La importancia de una **arquitectura modular** desde el inicio: separar rutas, controladores y middlewares hace el código más mantenible y preparado para escalar hacia los módulos 7 (base de datos + ORM) y 8 (API RESTful + JWT).

---

## Próximas etapas

- **Módulo 7:** Conexión a base de datos (PostgreSQL/MongoDB), modelos con Sequelize/Mongoose, operaciones CRUD.
- **Módulo 8:** API RESTful con autenticación JWT, subida de archivos con Multer.
# Modulo_6_7_8_JS
