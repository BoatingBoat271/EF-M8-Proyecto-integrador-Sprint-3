# KanbanPro

Aplicacion Kanban full-stack con autenticacion JWT, API REST segura y dashboard web conectado a PostgreSQL con Sequelize.

Ideal para demostrar un flujo real de producto: registro/login, gestion de trabajo por tableros y datos persistentes por usuario.

## Por que este proyecto es vendible

- Resuelve una necesidad real: organizar tareas por tableros, listas y tarjetas.
- Tiene arquitectura profesional: Express + Sequelize + PostgreSQL.
- Incluye seguridad moderna: autenticacion con JWT y rutas protegidas.
- Entrega experiencia completa: API para integraciones + interfaz web para uso diario.
- Es escalable: base clara para agregar equipos, etiquetas, fechas y reportes.

## Stack tecnologico

- Backend: Node.js + Express
- Base de datos: PostgreSQL
- ORM: Sequelize
- Auth: JWT + bcryptjs
- Vistas: Handlebars (hbs)

## Funcionalidades principales

- Registro e inicio de sesion de usuarios.
- Generacion de token JWT y validacion de acceso.
- CRUD completo de tableros.
- CRUD completo de listas dentro de cada tablero.
- CRUD completo de tarjetas dentro de cada lista.
- Dashboard con datos reales del usuario autenticado.

## Requisitos

- Node.js 18+ recomendado
- PostgreSQL activo
- Archivo `.env` en la raiz del proyecto

### Variables de entorno minimas

```env
DB_HOST=localhost
DB_PORT=5432
DB_NAME=Kanbanpro2
DB_USER=postgres
DB_PASSWORD=postgres
JWT_SECRET=kanbanpro_secret_sprint3
JWT_EXPIRES_IN=2h
```

## Inicio rapido

```bash
npm install
npm run db:create
npm run seed
npm run dev
```

La app quedara disponible en:

- Web: `http://localhost:3000`
- API base: `http://localhost:3000/api`

## Scripts disponibles

- `npm run start`: inicia en modo produccion.
- `npm run dev`: inicia con nodemon (desarrollo).
- `npm run db:create`: crea la base si no existe.
- `npm run seed`: carga datos semilla.
- `npm run test:crud`: prueba CRUD basica.

Tip si ejecutas comandos desde otra carpeta:

```bash
npm --prefix "c:\\Users\\pablo\\OneDrive\\Documentos\\EF-M8 Proyecto integrador Sprint 3" run dev
```

## Flujo de uso (API)

1. Registrar usuario: `POST /api/auth/register`
2. Iniciar sesion: `POST /api/auth/login`
3. Copiar token recibido en la respuesta
4. Enviar header en rutas protegidas:

```http
Authorization: Bearer TU_TOKEN
```

5. Consumir CRUD de tableros, listas y tarjetas

## Endpoints principales

### Auth

- `POST /api/auth/register`
  - Body JSON: `{ "email": "usuario@mail.com", "password": "12345678" }`
- `POST /api/auth/login`
  - Body JSON: `{ "email": "usuario@mail.com", "password": "12345678" }`
  - Respuesta esperada: `{ "ok": true, "token": "..." }`

### Tableros (protegido)

- `GET /api/tableros`
- `POST /api/tableros`
  - Body JSON: `{ "nombre": "Mi tablero", "descripcion": "Texto" }`
- `PUT /api/tableros/:id`
- `DELETE /api/tableros/:id`

### Listas (protegido)

- `POST /api/tableros/:tableroId/listas`
  - Body JSON: `{ "nombre": "Pendiente", "orden": 1 }`
- `PUT /api/tableros/:tableroId/listas/:id`
- `DELETE /api/tableros/:tableroId/listas/:id`

### Tarjetas (protegido)

- `POST /api/listas/:listaId/tarjetas`
  - Body JSON: `{ "titulo": "Tarea", "descripcion": "Detalle", "prioridad": "Media" }`
- `PUT /api/listas/:listaId/tarjetas/:id`
- `DELETE /api/listas/:listaId/tarjetas/:id`

## Dashboard web

1. Ir a `/login`
2. Iniciar sesion con credenciales validas
3. El sistema redirige a `/dashboard?token=...`
4. Se valida el token y se cargan tableros, listas y tarjetas del usuario

## Proximos pasos recomendados

- Agregar control de roles y permisos.
- Implementar filtros por prioridad y fechas.
- Incorporar drag & drop en el dashboard.
- Preparar despliegue con Docker.
