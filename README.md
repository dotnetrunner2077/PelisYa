# 🎬 PelisYa

**PelisYa** es una aplicación web completa para la gestión y registro de películas, que integra información detallada desde la API de IMDb. Permite a los usuarios registrar, consultar y administrar películas con información actualizada sobre actores, descripciones, portadas y puntuaciones.

> 📌 Proyecto final de DIgit@lers

## 📋 Tabla de Contenidos

- [Características](#-características)
- [Arquitectura](#-arquitectura)
- [Tecnologías](#-tecnologías)
- [Estructura del Proyecto](#-estructura-del-proyecto)
- [Requisitos Previos](#-requisitos-previos)
- [Configuración](#-configuración)
- [Instalación](#-instalación)
- [Uso](#-uso)
- [API Endpoints](#-api-endpoints)
- [Base de Datos](#-base-de-datos)

## ✨ Características

### Gestión de Películas
- ✅ Registro de películas con información completa
- ✅ Integración con **RapidAPI (IMDb)** para obtener datos automáticamente
- ✅ Actualización automática de portadas de películas
- ✅ Información detallada: actores principales, secundarios, descripción, fecha de estreno
- ✅ Almacenamiento del ID de IMDb para referencia

### Gestión de Usuarios
- ✅ Sistema de autenticación y autorización
- ✅ Manejo de sesiones seguras
- ✅ Diferentes roles de usuario
- ✅ Registro y login de usuarios

### Administración
- ✅ Categorización de contenido
- ✅ Sistema de listas personalizadas
- ✅ Gestión de facturas por cobrar
- ✅ Panel de control administrativo

## 🏗️ Arquitectura

La aplicación sigue una **arquitectura en capas** (N-Tier Architecture) con separación clara de responsabilidades:

```
PelisYa/
├── Web/              # Capa de Presentación (Razor Pages)
├── Api/              # Capa de Servicios (Web API)
├── Business/         # Capa de Lógica de Negocio
└── EntityLib/        # Capa de Acceso a Datos (Entity Framework Core)
```

### Flujo de la Aplicación

1. **Capa Web (Razor Pages)** → Interfaz de usuario con vistas y controladores
2. **Capa API (Web API)** → Endpoints RESTful para operaciones CRUD
3. **Capa Business** → Lógica de negocio, DTOs y mapeos
4. **Capa EntityLib** → Modelos de datos y contexto de Entity Framework

## 🛠️ Tecnologías

### Backend
- **.NET 6** - Framework principal
- **ASP.NET Core Razor Pages** - Interfaz web
- **ASP.NET Core Web API** - Servicios REST
- **Entity Framework Core 6.0.8** - ORM
- **AutoMapper 11.0.1** - Mapeo objeto-objeto
- **MySQL** - Base de datos (Pomelo.EntityFrameworkCore.MySql 6.0.2)

### Seguridad
- **JWT Bearer Authentication** - Autenticación basada en tokens
- **ASP.NET Core Identity** - Gestión de usuarios
- **Sesiones seguras** - Manejo de estado del usuario

### Integraciones
- **RapidAPI (IMDb)** - API de información de películas
- **Swagger/OpenAPI** - Documentación de API

### Herramientas
- **Code First Migrations** - Gestión de base de datos
- **Dependency Injection** - Inyección de dependencias

## 📁 Estructura del Proyecto

```
PelisYa/
│
├── Web/                                    # Proyecto Razor Pages
│   ├── Controllers/
│   │   ├── PeliculasController.cs         # Gestión de películas
│   │   ├── UsuariosController.cs          # Gestión de usuarios
│   │   ├── UserAccountController.cs       # Autenticación
│   │   └── HomeController.cs              # Página principal
│   ├── Models/
│   │   ├── PeliculasModel.cs
│   │   ├── UsuariosModel.cs
│   │   └── UserAccountModel.cs
│   ├── Helpers/
│   │   ├── ActionHelpers.cs               # Helpers para HTTP requests
│   │   ├── SessionsHelpers.cs             # Manejo de sesiones
│   │   └── LocalStorageHelpers.cs
│   └── Program.cs
│
├── Api/                                    # Proyecto Web API
│   ├── Controllers/
│   │   ├── PeliculasController.cs         # Endpoints de películas
│   │   ├── UsuariosController.cs          # Endpoints de usuarios
│   │   ├── CategoriasController.cs        # Endpoints de categorías
│   │   └── UserAccountController.cs       # Endpoints de autenticación
│   ├── appsettings.json
│   ├── settings.json                      # Configuración de conexión
│   └── Program.cs
│
├── Business/                               # Lógica de Negocio
│   ├── Peliculas/
│   │   └── PeliculasBusiness.cs           # Lógica de películas
│   ├── Usuarios/
│   │   └── UsuariosBusiness.cs            # Lógica de usuarios
│   ├── Categorias/
│   │   └── CategoriasBusiness.cs          # Lógica de categorías
│   ├── UserAccount/
│   │   └── UserAccountBusiness.cs         # Lógica de autenticación
│   ├── DTOs/
│   │   ├── PeliculasDTO.cs
│   │   ├── UsuariosDTO.cs
│   │   ├── CategoriasDTO.cs
│   │   └── ErrorDto.cs
│   └── Mappers/
│       └── UsuariosMapper.cs
│
└── EntityLib/                              # Capa de Datos
    ├── Peliculas.cs                       # Entidad Películas
    ├── Usuarios.cs                        # Entidad Usuarios
    ├── Categoriacontenido.cs              # Categorías de contenido
    ├── Categoriasusuarios.cs              # Categorías de usuarios
    ├── Series.cs                          # Entidad Series
    ├── Listas.cs                          # Listas de usuario
    ├── Subcategorias.cs                   # Subcategorías
    ├── Facturasporcobrar.cs               # Facturas
    ├── Estadofactura.cs                   # Estados de factura
    ├── pelisyaContext.cs                  # DbContext
    ├── Migrations/                        # Migraciones EF Core
    └── settings.json                      # Configuración de conexión
```

## 📦 Requisitos Previos

- **.NET 6 SDK** o superior
- **MySQL Server 8.0.23** o superior
- **Visual Studio 2022** o **Visual Studio Code**
- **Cuenta de RapidAPI** con acceso a la API de IMDb (movie-details1)

## ⚙️ Configuración

### 1. Configurar la Base de Datos

Crear un archivo `settings.json` en los proyectos **Api** y **EntityLib**:

```json
{
  "ConnectionStringDesarrollo": "server=localhost;port=3306;database=pelisya;user=tu_usuario;password=tu_password"
}
```

### 2. Configurar RapidAPI

En `Web/appsettings.Development.json`:

```json
{
  "apiUrl": "https://localhost:7XXX/api/",
  "RapidAPIKey": "TU_RAPID_API_KEY",
  "RapidAPIHost": "movie-details1.p.rapidapi.com"
}
```

### 3. Configurar JWT Authentication

En `Api/appsettings.Development.json`:

```json
{
  "Authentication": {
    "SecretKey": "TU_CLAVE_SECRETA_MINIMO_32_CARACTERES"
  }
}
```

## 🚀 Instalación

### 1. Clonar el repositorio

```bash
git clone https://github.com/dotnetrunner2077/PelisYa.git
cd PelisYa
```

### 2. Restaurar paquetes NuGet

```bash
dotnet restore
```

### 3. Aplicar migraciones (opcional, si usas Code First)

```bash
cd EntityLib
dotnet ef database update
```

### 4. Ejecutar la API

```bash
cd Api
dotnet run
```

La API estará disponible en: `https://localhost:7XXX`

### 5. Ejecutar la aplicación Web

En otra terminal:

```bash
cd Web
dotnet run
```

La aplicación web estará disponible en: `https://localhost:7XXX`

## 📖 Uso

### Registrar una Película con IMDb

1. **Iniciar sesión** en la aplicación
2. Navegar a **"Películas" → "Crear"**
3. Ingresar el **ID de IMDb** (ej: `tt0111161` para "The Shawshank Redemption")
4. Click en **"Buscar en IMDb"**
5. La aplicación automáticamente:
   - Obtiene el título, descripción, fecha de estreno
   - Descarga los actores principales y secundarios
   - Obtiene la URL de la portada
6. **Guardar** la película

### Visualizar Películas

- La página de **"Películas"** muestra todas las películas registradas
- Las portadas se actualizan automáticamente si no están disponibles
- Se puede filtrar por categorías

## 🔌 API Endpoints

### Películas

```http
GET    /api/Peliculas              # Obtener todas las películas
POST   /api/Peliculas              # Crear una película
PUT    /api/Peliculas              # Actualizar una película
```

### Usuarios

```http
GET    /api/Usuarios               # Obtener todos los usuarios
POST   /api/Usuarios               # Crear un usuario
PUT    /api/Usuarios               # Actualizar un usuario
```

### Categorías

```http
GET    /api/Categorias             # Obtener todas las categorías
POST   /api/Categorias             # Crear una categoría
```

### Autenticación

```http
POST   /api/UserAccount/Login      # Iniciar sesión (retorna JWT)
POST   /api/UserAccount/Register   # Registrar nuevo usuario
```

### Ejemplo de Request - Crear Película

```json
POST /api/Peliculas
Content-Type: application/json

{
  "idCategoriaPeliculas": 1,
  "nombre": "The Shawshank Redemption",
  "descripcion": "Two imprisoned men bond over a number of years...",
  "fecha": "1994-09-23T00:00:00",
  "actorPrincipal": "Tim Robbins",
  "actorPrincipal2": "Morgan Freeman",
  "actorSecundario": "Bob Gunton",
  "actorSecundario2": "William Sadler",
  "idImdb": "tt0111161",
  "portada": "https://m.media-amazon.com/images/..."
}
```

## 🗄️ Base de Datos

### Entidades Principales

#### Peliculas
- `IdPelicula` (PK)
- `IdCategoriaPeliculas` (FK)
- `Nombre`
- `Descripcion`
- `Fecha`
- `ActorPrincipal`, `ActorPrincipal2`
- `ActorSecundario`, `ActorSecundario2`
- `IdImdb` - ID único de IMDb
- `Portada` - URL de la imagen

#### Usuarios
- `IdUsuario` (PK)
- `IdCategoria` (FK)
- `Nombre`, `Apellido`
- `Email`, `Password`
- `FechaNacimiento`, `FechaAlta`

#### Categoriacontenido
- `IdCategoria` (PK)
- `Descripcion` - Acción, Comedia, Drama, etc.

#### Categoriasusuarios
- `IdCategoria` (PK)
- `Descripcion` - Admin, Usuario, Premium, etc.

### Diagrama Relacional

```
Categoriacontenido ──┐
                     ├── Peliculas ──┬── Listas
                     └── Series      └── Subcategorias

Categoriasusuarios ───── Usuarios ──┬── Listas
                                    └── Facturasporcobrar
```

## 🔐 Seguridad

- **Autenticación JWT** para proteger endpoints
- **Sesiones seguras** con cookies HttpOnly
- **Validación de roles** para acceso a funcionalidades
- **Password hashing** para almacenamiento seguro
- **CORS configurado** para peticiones cross-origin

## 🤝 Contribuciones

Las contribuciones son bienvenidas. Por favor:

1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📝 Notas

- La aplicación está configurada para usar **MySQL**, pero puede adaptarse a otros proveedores cambiando el DbContext
- Se recomienda usar **HTTPS** en producción
- Los archivos `settings.json` y claves de API no deben incluirse en el repositorio (usar `.gitignore`)

## 📧 Contacto

**Proyecto:** [PelisYa](https://github.com/dotnetrunner2077/PelisYa)

**Autor:** dotnetrunner2077

---

⭐ Si te gusta este proyecto, ¡dale una estrella en GitHub!
