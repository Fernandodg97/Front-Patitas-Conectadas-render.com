# Patitas Conectadas 🐾

Frontend de la red social para dueños de mascotas **Patitas Conectadas**. Construido con React 19 + TypeScript, consume la [API REST](https://github.com/Fernandodg97/API-PatitasConectadas-Docker) desarrollada con Spring Boot 3 y desplegada en Render.

> **Demo en producción** → [api-patitasconectadas-docker.onrender.com](https://api-patitasconectadas-docker.onrender.com/swagger-ui/index.html)  
> Usuario de prueba: `usuario@usuario.com` · Contraseña: `usuario`

---

## Características

- **🔒 Autenticación JWT** — Registro, login y rutas protegidas. El token se guarda en `localStorage` bajo la clave `auth_token`
- **🏠 Feed Social** — Publicaciones con imagen, comentarios y reacciones
- **👥 Red de Amigos** — Seguir usuarios, gestionar seguidores y buscador de usuarios
- **🐾 Mascotas** — Registrar y administrar mascotas por perfil con foto
- **📅 Eventos** — Crear, descubrir y apuntarse a eventos de la comunidad
- **👥 Grupos** — Unirse y gestionar grupos temáticos con roles (Admin / Miembro)
- **💾 Posts Guardados** — Guardar publicaciones para consultar después
- **🔔 Notificaciones** — Centro de notificaciones con dropdown
- **💬 Chat** — Mensajería directa entre usuarios con estado visto/no visto
- **🏢 Protectoras** — Sección dedicada a organizaciones de rescate

---

## Stack Tecnológico

| Categoría | Tecnología |
|---|---|
| UI | React 19 + TypeScript |
| Build | Vite 6 |
| Estilos | Tailwind CSS |
| Routing | React Router v6 |
| HTTP | Axios |
| Notificaciones UI | React Toastify |
| Emojis | Emoji Picker React |
| Fechas | date-fns |
| Iconos | React Icons |

**Backend asociado:** Java 21 · Spring Boot 3 · Spring Security · JWT · PostgreSQL (Supabase) · Cloudinary · Docker

---

## Integración con la API

### URL base

```
https://api-patitasconectadas-docker.onrender.com
```

Configurable mediante la variable de entorno `VITE_API_URL`. Si no se define, el frontend apunta a la instancia de producción en Render.

### Autenticación

1. `POST /auth/register` — Registro de nuevo usuario
2. `POST /auth/login` — Devuelve un **token JWT**
3. El token se almacena en `localStorage` (`auth_token`) y se envía en cada petición:

```
Authorization: Bearer <token>
```

4. `GET /auth/me` — Devuelve el usuario autenticado con su perfil y mascotas

### Imágenes (Cloudinary)

Las imágenes se almacenan en **Cloudinary**. Los endpoints que aceptan imagen usan `multipart/form-data`. El campo devuelto es siempre una URL pública:

```
https://res.cloudinary.com/<cloud>/image/upload/v.../nombre.jpg
```

| Recurso | Campo | Límite |
|---|---|---|
| Posts | `img` | 10 MB |
| Mascotas | `foto` | 10 MB |
| Perfiles | `img` | 10 MB |
| Comentarios | `img` | 10 MB |

Tipos permitidos: `image/jpeg`, `image/png`, `image/gif`, `image/webp`

> Al actualizar o eliminar un recurso, la imagen anterior se borra automáticamente de Cloudinary.

### Endpoints principales consumidos

| Módulo | Endpoints |
|---|---|
| Auth | `POST /auth/login`, `POST /auth/register`, `GET /auth/me` |
| Usuarios | `GET /usuarios`, `GET /usuarios/{id}`, `PUT /usuarios/{id}`, `PATCH /usuarios/{id}/password`, `POST /usuarios/restablecer-contrasena` |
| Perfiles | `GET /usuarios/{id}/perfiles`, `PUT /usuarios/{id}/perfiles` |
| Posts | `GET /posts`, `POST /posts`, `PUT /posts/{id}`, `DELETE /posts/{id}`, `GET /usuarios/{id}/posts` |
| Comentarios | `GET /posts/{id}/comentarios`, `POST /posts/{id}/comentarios`, `DELETE /comentarios/{id}` |
| Mascotas | `GET /usuarios/{id}/mascotas`, `POST /usuarios/{id}/mascotas`, `PUT /usuarios/{id}/mascotas/{mascotaId}`, `DELETE /usuarios/{id}/mascotas/{mascotaId}` |
| Chat | `POST /chat/enviar`, `GET /chat/conversacion/{u1}/{u2}`, `PUT /chat/marcar-vistos/{u1}/{u2}`, `GET /chat/no-vistos/{id}` |
| Eventos | `GET /eventos`, `POST /eventos`, `PUT /eventos/{id}`, `DELETE /eventos/{id}` |
| Grupos | `GET /grupos`, `POST /grupos`, `PUT /grupos/{id}`, `DELETE /grupos/{id}` |
| Seguidos | `GET /usuarios/{id}/seguidos`, `POST /usuarios/{id}/seguidos/{seguidoId}`, `DELETE /usuarios/{id}/seguidos/{seguidoId}` |
| Valoraciones | `POST /valoraciones/usuarios/{autorId}/receptor/{receptorId}`, `GET /valoraciones/usuarios/{id}/recibidas` |
| Notificaciones | `GET /notificaciones`, `DELETE /notificaciones/{id}` |
| Guardados | `GET /usuario-post/usuario/{id}`, `POST /usuario-post`, `DELETE /usuario-post/{id}` |

> Documentación interactiva completa del backend en [`/swagger-ui/index.html`](https://api-patitasconectadas-docker.onrender.com/swagger-ui/index.html)

---

## Instalación

### Requisitos Previos
- Node.js v18+
- npm

### Pasos

1. Clonar el repositorio
   ```bash
   git clone https://github.com/Fernandodg97/Front-Patitas-Conectadas-render.com.git
   cd Front-Patitas-Conectadas-render.com
   ```

2. Instalar dependencias
   ```bash
   npm install
   ```

3. Configurar variables de entorno *(opcional — por defecto apunta a producción)*
   ```env
   VITE_API_URL=http://localhost:8080
   ```

4. Iniciar el servidor de desarrollo
   ```bash
   npm run dev
   ```
   Disponible en `http://localhost:5173`

5. Build de producción
   ```bash
   npm run build
   ```

### Levantar el backend en local

Consulta [API-PatitasConectadas-Docker](https://github.com/Fernandodg97/API-PatitasConectadas-Docker) para instrucciones completas. Resumen rápido con Docker:

```bash
git clone https://github.com/Fernandodg97/API-PatitasConectadas-Docker
cd API-PatitasConectadas-Docker

# Crear .env con las variables necesarias
docker build -t api-patitas .
docker run -p 8080:8080 --env-file .env api-patitas
```

Variables de entorno necesarias en el backend:
```env
DATABASE_URL=jdbc:postgresql://<host>/<db>?sslmode=require
DATABASE_USERNAME=...
DATABASE_PASSWORD=...
CLOUDINARY_CLOUD_NAME=...
CLOUDINARY_API_KEY=...
CLOUDINARY_API_SECRET=...
```

---

## Estructura del Proyecto

```
├── public/                  # Avatares y placeholders por defecto
├── src/
│   ├── assets/              # Logo e imágenes estáticas
│   ├── components/          # Componentes UI reutilizables
│   │   ├── amigos/          # Buscador y listados de amigos/seguidores
│   │   ├── auth/            # Login, Register, ProtectedRoute
│   │   ├── chat/            # ChatConversacion, MensajeItem
│   │   ├── common/          # Botones, spinners, diálogos, EmojiPicker
│   │   ├── eventos/         # EventoForm, EventosList, ParticipantesEvento
│   │   ├── feed/            # Feed "Para Ti"
│   │   ├── groups/          # GrupoCard, GrupoDetalle, GrupoForm, MiembrosGrupo
│   │   ├── home/            # PostItem, PostForm, CommentSection y utilidades
│   │   ├── layout/          # Navbar, Sidebar, MobileBottomNav, MainLayout
│   │   ├── notificaciones/  # NotificacionesDropdown, NotificacionItem
│   │   ├── post/            # Componentes de post individual
│   │   ├── profile/         # ProfileHeader, ProfileDetails, MascotasList, etc.
│   │   ├── routes/          # AppRoutes
│   │   └── Savedposts/      # PostCard y ComentariosLista
│   ├── context/             # AuthContext (JWT), UserContext
│   ├── routes/              # Índice de rutas
│   ├── services/            # Servicios Axios por módulo (api.ts, postService.ts…)
│   ├── types/               # Tipos TypeScript (Post, etc.)
│   ├── utils/               # Funciones utilitarias
│   ├── views/               # Vistas/páginas de la aplicación
│   ├── config.ts            # URL de la API, paginación y límites de subida
│   ├── App.tsx
│   └── main.tsx
├── puml/                    # Diagramas PlantUML de arquitectura
├── eslint.config.js
├── tailwind.config.js
├── vite.config.ts
└── package.json
```

---

## Scripts Disponibles

```bash
npm run dev       # Servidor de desarrollo (http://localhost:5173)
npm run build     # Build de producción
npm run preview   # Preview del build
npm run lint      # Linter ESLint
```

---

## Repositorios del Proyecto

| Repositorio | Descripción |
|---|---|
| [Front-Patitas-Conectadas-render.com](https://github.com/Fernandodg97/Front-Patitas-Conectadas-render.com) | Este repositorio — React + TypeScript |
| [API-PatitasConectadas-Docker](https://github.com/Fernandodg97/API-PatitasConectadas-Docker) | Backend — Spring Boot 3 + Docker |

---

## Licencia

[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.es)

---

<p align="center">Made with ❤️ for animals everywhere</p>
