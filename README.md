# Patitas Conectadas 🐾

## Descripción
Patitas Conectadas es una plataforma web social que conecta refugios de animales, organizaciones de rescate, adoptantes y amantes de los animales en un ecosistema unificado. Su misión es agilizar el proceso de adopción de mascotas y crear una comunidad solidaria para el bienestar animal.

## Características Principales
- **🔒 Sistema de Autenticación**: Registro, inicio de sesión y rutas protegidas
- **🏠 Feed Social**: Publicaciones, comentarios y reacciones entre usuarios
- **👥 Red de Amigos**: Seguir usuarios, gestionar amigos y seguidores
- **🐾 Gestión de Mascotas**: Registrar y administrar mascotas por perfil
- **📅 Eventos**: Crear, descubrir y participar en eventos de la comunidad
- **👥 Grupos**: Unirse y gestionar grupos temáticos
- **💾 Posts Guardados**: Guardar publicaciones para consultar después
- **🔔 Notificaciones**: Centro de notificaciones con dropdown
- **💬 Chat**: Sistema de mensajería entre usuarios
- **🏢 Protectoras**: Sección dedicada a organizaciones de rescate

## Stack Tecnológico
- **Frontend**: React 19 con TypeScript
- **Build Tool**: Vite 6
- **Styling**: Tailwind CSS
- **Routing**: React Router v6 con rutas protegidas
- **HTTP Client**: Axios
- **Notificaciones UI**: React Toastify
- **Emojis**: Emoji Picker React
- **Fechas**: date-fns
- **Iconos**: React Icons

## Instalación

### Requisitos Previos
- Node.js (v18.0.0 o superior)
- npm

### Pasos de Instalación

1. Clonar el repositorio
   ```bash
   git clone https://github.com/Fernandodg97/Front-Patitas-Conectadas-render.com.git
   cd Front-Patitas-Conectadas-render.com
   ```

2. Instalar dependencias
   ```bash
   npm install
   ```

3. Configurar variables de entorno  
   Crear un archivo `.env` en la raíz del proyecto:
   ```
   VITE_API_URL=tu_endpoint_api
   ```

4. Iniciar el servidor de desarrollo
   ```bash
   npm run dev
   ```
   La aplicación estará disponible en `http://localhost:5173/`

5. Construir para producción
   ```bash
   npm run build
   ```

## Estructura del Proyecto
```
├── public/                  # Archivos estáticos e imágenes por defecto
├── src/
│   ├── assets/              # Imágenes y recursos estáticos
│   ├── components/          # Componentes UI reutilizables
│   │   ├── amigos/          # Buscador y listados de amigos/seguidores
│   │   ├── auth/            # Login, Register, rutas protegidas
│   │   ├── chat/            # Conversación y mensajes
│   │   ├── common/          # Botones, spinners, diálogos compartidos
│   │   ├── eventos/         # Formulario y listado de eventos
│   │   ├── feed/            # Feed "Para Ti"
│   │   ├── groups/          # Grupos, miembros y formularios
│   │   ├── home/            # Posts, comentarios y formularios del home
│   │   ├── layout/          # Navbar, Sidebar, MobileBottomNav, MainLayout
│   │   ├── notificaciones/  # Dropdown e ítems de notificaciones
│   │   ├── post/            # Componentes de post individual
│   │   ├── profile/         # Header, detalles, mascotas y acciones del perfil
│   │   ├── routes/          # AppRoutes (definición de rutas)
│   │   └── Savedposts/      # PostCard y comentarios de posts guardados
│   ├── context/             # AuthContext, UserContext
│   ├── routes/              # Índice de rutas
│   ├── services/            # Servicios de API (axios)
│   ├── types/               # Tipos TypeScript
│   ├── utils/               # Funciones utilitarias
│   ├── views/               # Páginas/vistas de la aplicación
│   │   ├── Amigos.tsx
│   │   ├── Chat.tsx
│   │   ├── Configuracion.tsx
│   │   ├── Eventos.tsx
│   │   ├── Grupos.tsx
│   │   ├── Guardados.tsx
│   │   ├── Home.tsx
│   │   ├── NotFound.tsx
│   │   ├── Notificaciones.tsx
│   │   ├── Perfil.tsx
│   │   ├── Profile.tsx
│   │   ├── Protectoras.tsx
│   │   └── RecuperarContrasena.tsx
│   ├── config.ts            # Configuración global (base URL, etc.)
│   ├── App.tsx              # Componente raíz
│   ├── main.tsx             # Punto de entrada
│   └── vite-env.d.ts        # Tipos de Vite
├── puml/                    # Diagramas PlantUML de arquitectura
├── eslint.config.js
├── tailwind.config.js
├── vite.config.ts
├── tsconfig.json
└── package.json
```

## Scripts Disponibles
```bash
npm run dev       # Servidor de desarrollo
npm run build     # Build de producción
npm run preview   # Preview del build
npm run lint      # Linter ESLint
```

## Contribuir

1. Haz fork del repositorio
2. Crea tu rama de feature (`git checkout -b feature/nueva-funcionalidad`)
3. Haz commit de tus cambios (`git commit -m 'feat: descripción del cambio'`)
4. Push a la rama (`git push origin feature/nueva-funcionalidad`)
5. Abre un Pull Request

## Licencia
Este proyecto está licenciado bajo la Licencia MIT.

---

<p align="center">Made with ❤️ for animals everywhere</p>
