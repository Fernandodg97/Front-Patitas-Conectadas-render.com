# Patitas Conectadas — Frontend 🐾

[![React](https://img.shields.io/badge/React_19-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)](https://reactjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Vite](https://img.shields.io/badge/Vite_6-646CFF?style=for-the-badge&logo=vite&logoColor=white)](https://vitejs.dev/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)

Frontend de la red social para dueños de mascotas **Patitas Conectadas**. SPA construida con React 19 y TypeScript, con autenticación JWT, subida de imágenes a Cloudinary y consumo de una API REST propia en Spring Boot. Desplegada en producción en Render.

> **🌐 Demo app** → [front-patitas-conectadas-render-com.onrender.com](https://front-patitas-conectadas-render-com.onrender.com)  
> Usuario de prueba: `usuario@usuario.com` · Contraseña: `usuario` · ⏱️ Los servicios pueden tardar ~30s en arrancar (plan gratuito de Render).

---

### 👋 Para recruiters

Frontend completo de una red social para dueños de mascotas, construido de cero e integrado con una API REST propia en Spring Boot.

**¿Qué demuestra este repositorio?**

- ✅ Construir una SPA en **React 19 + TypeScript** con arquitectura modular (vistas, componentes, servicios, contextos)
- ✅ Implementar **autenticación JWT** con rutas protegidas y persistencia de sesión
- ✅ Consumir una API REST con **Axios**, incluyendo subida de imágenes `multipart/form-data` a Cloudinary
- ✅ Aplicar **diseño responsive** con Tailwind CSS — navegación adaptada a móvil y escritorio
- ✅ Desplegar en **producción** como static site en Render, conectado a un backend dockerizado

| | |
|---|---|
| 🌐 **App en producción** | [front-patitas-conectadas-render-com.onrender.com](https://front-patitas-conectadas-render-com.onrender.com) |
| 🔧 **API (Swagger)** | [api-patitasconectadas-docker.onrender.com/swagger-ui](https://api-patitasconectadas-docker.onrender.com/swagger-ui/index.html) |
| 🗄️ **Repositorio backend** | [API-PatitasConectadas-Docker](https://github.com/Fernandodg97/API-PatitasConectadas-Docker) |
| 📋 **Proyecto general (TFG)** | [Patitas-Conectadas](https://github.com/Fernandodg97/Patitas-Conectadas) |

> ⏱️ Usuario demo: `usuario@usuario.com` · Contraseña: `usuario` · Los servicios pueden tardar ~30s en arrancar (plan gratuito de Render).

---

## 🚀 Mejoras Post-Práctica

El TFG entregado funcionaba en local. Tras la defensa, Fernando continuó de forma autónoma para llevarlo a producción real:

| Mejora | Detalle |
|---|---|
| ☁️ **Despliegue en producción** | Frontend desplegado como static site en Render, con build de Vite optimizado |
| 🖼️ **Integración Cloudinary** | Subida de imágenes `multipart/form-data` al backend, que delega en Cloudinary y devuelve la URL pública |
| 🔗 **Soporte URLs remotas** | Adaptación para manejar URLs completas de Cloudinary devueltas por la nueva versión del backend |
| 🗄️ **Conexión a Supabase** | La API consume PostgreSQL en Supabase — el frontend no requiere ninguna base de datos local para funcionar |

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

**Backend asociado:** Java 21 · Spring Boot 3 · Spring Security + JWT · PostgreSQL (Supabase) · Cloudinary · Docker

---

## Funcionalidades implementadas

| Módulo | Descripción |
|---|---|
| **Feed** | Publicaciones con imagen, comentarios y reacciones |
| **Perfil** | Foto, bio, mascotas, seguidores/seguidos y valoraciones 1–5 ⭐ |
| **Amigos** | Seguir usuarios, gestionar seguidores y buscador por nombre |
| **Mascotas** | Registro con foto, especie, género y fecha de nacimiento |
| **Eventos** | Crear y apuntarse a eventos con ubicación y fecha |
| **Grupos** | Comunidades con roles Administrador / Miembro y posts propios |
| **Chat** | Mensajería directa con estado visto/no visto |
| **Notificaciones** | Centro de notificaciones con dropdown por usuario |
| **Posts guardados** | Guardar publicaciones para consultar después |
| **Protectoras** | Sección dedicada a organizaciones de rescate animal |

---

## Retos técnicos resueltos

**Autenticación y sesión** — JWT almacenado en `localStorage`, adjuntado automáticamente en cada request con Axios. Rutas protegidas con `ProtectedRoute` que redirige al login si no hay sesión activa.

**Arquitectura modular** — Separación clara entre vistas (`/views`), componentes reutilizables (`/components`), servicios de API (`/services`), contextos globales (`/context`) y tipos TypeScript (`/types`).

**Subida de imágenes** — Los formularios de posts, mascotas y perfil envían `multipart/form-data` al backend, que gestiona la subida a Cloudinary y devuelve la URL pública. El frontend muestra la imagen directamente desde Cloudinary.

**Responsive** — Dos modos de navegación: `Sidebar` en escritorio y `MobileBottomNav` en móvil, construidos íntegramente con Tailwind CSS sin librerías externas de layout.

**Gestión de estado** — `AuthContext` para la sesión del usuario y `UserContext` para los datos del perfil activo, accesibles desde cualquier componente sin prop drilling.

---

## Integración con la API

### URL base

```
https://api-patitasconectadas-docker.onrender.com
```

Configurable mediante `VITE_API_URL`. Si no se define, apunta a la instancia de producción.

### Flujo de autenticación

```
POST /auth/login  →  { token: "eyJ..." }
                          │
                    localStorage["auth_token"]
                          │
              Authorization: Bearer <token>  →  cualquier endpoint protegido
```

### Imágenes (Cloudinary)

Los endpoints que aceptan imagen usan `multipart/form-data`. La respuesta incluye siempre una URL pública:

```
https://res.cloudinary.com/<cloud>/image/upload/v.../nombre.jpg
```

| Recurso | Campo | Límite |
|---|---|---|
| Posts | `img` | 10 MB |
| Mascotas | `foto` | 10 MB |
| Perfiles | `img` | 10 MB |

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

> Documentación interactiva completa en [`/swagger-ui/index.html`](https://api-patitasconectadas-docker.onrender.com/swagger-ui/index.html)

---

## Instalación

### Requisitos
- Node.js v18+
- npm

### Pasos

```bash
git clone https://github.com/Fernandodg97/Front-Patitas-Conectadas-render.com.git
cd Front-Patitas-Conectadas-render.com
npm install
npm run dev
```

Disponible en `http://localhost:5173`. Por defecto apunta a la API en producción.

Para apuntar al backend en local, crea un `.env`:

```env
VITE_API_URL=http://localhost:8080
```

### Levantar el backend en local

```bash
git clone https://github.com/Fernandodg97/API-PatitasConectadas-Docker
cd API-PatitasConectadas-Docker
# Crear .env con DATABASE_URL, DATABASE_USERNAME, DATABASE_PASSWORD, CLOUDINARY_*
docker build -t api-patitas .
docker run -p 8080:8080 --env-file .env api-patitas
```

---

## Estructura del Proyecto

```
├── public/                  # Avatares y placeholders por defecto
├── src/
│   ├── components/          # Componentes UI reutilizables
│   │   ├── amigos/          # Buscador y listados de amigos/seguidores
│   │   ├── auth/            # Login, Register, ProtectedRoute
│   │   ├── chat/            # ChatConversacion, MensajeItem
│   │   ├── common/          # Botones, spinners, diálogos, EmojiPicker
│   │   ├── eventos/         # EventoForm, EventosList, ParticipantesEvento
│   │   ├── groups/          # GrupoCard, GrupoDetalle, GrupoForm, MiembrosGrupo
│   │   ├── home/            # PostItem, PostForm, CommentsSection y utilidades
│   │   ├── layout/          # Navbar, Sidebar, MobileBottomNav, MainLayout
│   │   ├── notificaciones/  # NotificacionesDropdown, NotificacionItem
│   │   ├── profile/         # ProfileHeader, ProfileDetails, MascotasList
│   │   └── Savedposts/      # PostCard y ComentariosLista
│   ├── context/             # AuthContext (JWT), UserContext
│   ├── services/            # Servicios Axios por módulo
│   ├── views/               # Vistas/páginas de la aplicación
│   ├── types/               # Tipos TypeScript
│   ├── utils/               # Funciones utilitarias
│   └── config.ts            # URL base, paginación y límites de subida
├── puml/                    # Diagramas PlantUML de arquitectura
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

## Autores

| | |
|---|---|
| **Fernando Diaz** | [github.com/Fernandodg97](https://github.com/Fernandodg97) |
| **Mouad Sedjari** | [github.com/Msedjari](https://github.com/Msedjari) |

---

## Licencia

[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.es)

---

<p align="center">Made with ❤️ for animals everywhere</p>
