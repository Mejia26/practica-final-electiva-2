# DevOps Task Manager - Proyecto Final Electiva 2 ITLA

Una aplicación web avanzada de gestión de tareas construida con tecnologías modernas, implementando un pipeline completo de CI/CD para despliegue automatizado y monitoreo continuo.

## Características Principales

### 🎨 Interfaz de Usuario Avanzada
- **Animaciones 3D Interactivas**: Fondo con partículas Three.js que responden al movimiento del mouse
- **Animaciones GSAP**: Transiciones suaves y efectos visuales profesionales
- **Diseño Responsive**: Interfaz adaptativa con efectos de vidrio (backdrop-filter)
- **Elementos Flotantes**: Animaciones CSS autónomas para mayor dinamismo

### 🔧 Funcionalidades Técnicas
- **Gestión de Tareas**: CRUD completo (Crear, Leer, Eliminar) con SQLite en memoria
- **Monitoreo en Tiempo Real**: Endpoints de health check y métricas del sistema
- **Versionado Dinámico**: Muestra el commit SHA de Git para rastrear despliegues
- **Manejo de Errores**: Sistema robusto de notificaciones visuales

### 🚀 Pipeline DevOps Completo

#### Integración Continua (CI)
- **Automatización de Pruebas**: Ejecución automática de tests unitarios en cada push a la rama main
- **Control de Calidad**: Linting y validación de código con ESLint
- **Entorno de Pruebas**: Configuración automática de Node.js 18 en Ubuntu latest

#### Despliegue Continuo (CD)
- **Containerización**: Build automático de imágenes Docker con múltiples tags
  - `latest`: Versión más reciente
  - `SHA_SHORT`: Tag basado en el commit hash corto (ej: abc1234)
  - `DATE`: Tag basado en fecha (ej: 20260423)
- **Registro de Imágenes**: Push automático a Docker Hub
- **Despliegue en la Nube**: Trigger automático de despliegue en Render vía API
- **Versionado Inteligente**: Cada despliegue tiene un identificador único traceable

#### Infraestructura como Código
- **Docker**: Containerización completa de la aplicación
- **Render**: Plataforma de despliegue con escalado automático
- **GitHub Actions**: Orquestación del pipeline completo
- **Secrets Management**: Manejo seguro de credenciales (Docker Hub, Render API)

## Arquitectura Técnica

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   GitHub Push   │ -> │  GitHub Actions │ -> │   Docker Build  │
│    (main)       │    │   CI/CD Pipeline│    │   & Push Hub    │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                                                        │
                                                        v
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  Render Deploy  │ <- │   API Trigger   │ <- │  Docker Pull    │
│   Auto-scaling  │    │   Webhook       │    │   & Run         │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

## API Endpoints

### Gestión de Tareas
- `GET /api/tasks` - Lista todas las tareas
- `POST /api/tasks` - Crea una nueva tarea (body: `{ "title": "string" }`)
- `DELETE /api/tasks/:id` - Elimina una tarea por ID

### Monitoreo y Salud
- `GET /health` - Health check con versión del despliegue
- `GET /metrics` - Métricas del sistema (uptime, memoria, plataforma)
- `GET /api/version` - Versión actual basada en RENDER_GIT_COMMIT

## Tecnologías Utilizadas

### Backend
- **Node.js 18**: Runtime de JavaScript
- **Express.js**: Framework web minimalista
- **SQLite3**: Base de datos en memoria para persistencia ligera
- **Morgan**: Logging de requests HTTP
- **CORS**: Manejo de cross-origin requests

### Frontend
- **Three.js**: Biblioteca 3D para animaciones interactivas
- **GSAP**: Animaciones profesionales y transiciones
- **CSS3**: Estilos avanzados con gradientes, sombras y filtros
- **HTML5 Canvas**: Renderizado de gráficos 3D

### DevOps & Infraestructura
- **Docker**: Containerización de aplicaciones
- **GitHub Actions**: CI/CD pipeline automation
- **Render**: Plataforma de deployment cloud
- **Docker Hub**: Registro de imágenes container

### Testing
- **Jest**: Framework de testing JavaScript
- **Supertest**: Testing de APIs HTTP

## Instalación y Ejecución Local

### Prerrequisitos
- Node.js 18+
- Docker (opcional para containerización)

### Instalación
```bash
# Clonar el repositorio
git clone <repository-url>
cd practica-final-electiva-2

# Instalar dependencias
cd app
npm install
```

### Ejecución
```bash
# Ejecutar la aplicación
npm start

# Ejecutar tests
npm test

# Ejecutar linting
npm run lint
```

La aplicación estará disponible en `http://localhost:3000`

### Con Docker
```bash
# Build de la imagen
docker build -t devops-task-manager .

# Ejecutar el container
docker run -p 3000:3000 devops-task-manager
```

## Configuración del Pipeline CI/CD

### Variables de Entorno Requeridas
Para el funcionamiento completo del pipeline, configurar los siguientes secrets en GitHub:

- `DOCKER_USERNAME`: Usuario de Docker Hub
- `DOCKER_PASSWORD`: Password de Docker Hub
- `RENDER_SERVICE_ID`: ID del servicio en Render
- `RENDER_API_KEY`: API Key de Render

### Flujo del Pipeline
1. **Push a main** → Trigger automático
2. **CI Phase**: Setup Node.js, install deps, run tests
3. **CD Phase**: Build Docker image, push to registry, trigger Render deploy
4. **Deploy**: Render actualiza la aplicación automáticamente

## Monitoreo y Observabilidad

- **Health Checks**: Endpoint `/health` para verificación de estado
- **Métricas del Sistema**: `/metrics` proporciona datos de rendimiento
- **Version Tracking**: Badge visual muestra el commit del despliegue actual
- **Error Handling**: Logs detallados y notificaciones de errores

## Seguridad

- **Secrets Management**: Credenciales almacenadas de forma segura en GitHub Secrets
- **Input Validation**: Validación de datos en endpoints de API
- **Error Sanitization**: Mensajes de error no revelan información sensible
- **HTTPS**: Despliegue en Render con SSL automático

## Escalabilidad

- **Containerización**: Fácil escalado horizontal con Docker
- **Stateless Design**: Arquitectura sin estado para múltiples instancias
- **CDN Ready**: Assets optimizados para distribución global
- **Auto-scaling**: Render maneja escalado automático basado en demanda

---

**Proyecto Final - Electiva 2 DevOps - ITLA 2026**